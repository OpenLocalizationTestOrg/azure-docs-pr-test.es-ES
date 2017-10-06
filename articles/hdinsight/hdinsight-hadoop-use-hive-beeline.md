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
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="933bb-105">Usar el cliente de hello Beeline con Apache Hive</span><span class="sxs-lookup"><span data-stu-id="933bb-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="933bb-106">Obtenga información acerca de cómo toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) consultas toorun Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="933bb-107">BEELINE es un cliente de Hive que está incluido en los nodos principales del saludo de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="933bb-108">BEELINE usa JDBC tooconnect tooHiveServer2, un servicio hospedado en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="933bb-109">También puede utilizar Beeline tooaccess Hive en HDInsight de forma remota en Hola internet.</span><span class="sxs-lookup"><span data-stu-id="933bb-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="933bb-110">Hello en la tabla siguiente proporciona las cadenas de conexión para su uso con Beeline:</span><span class="sxs-lookup"><span data-stu-id="933bb-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="933bb-111">Desde dónde se ejecuta Beeline</span><span class="sxs-lookup"><span data-stu-id="933bb-111">Where you run Beeline from</span></span> | <span data-ttu-id="933bb-112">parameters</span><span class="sxs-lookup"><span data-stu-id="933bb-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="933bb-113">Un nodo de nodo principal o de borde del tooa de conexión de SSH</span><span class="sxs-lookup"><span data-stu-id="933bb-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="933bb-114">Clúster de hello exterior</span><span class="sxs-lookup"><span data-stu-id="933bb-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="933bb-115">Reemplace `admin` con la cuenta de inicio de sesión de clúster de hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="933bb-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="933bb-116">Reemplace `password` con contraseña de Hola de cuenta de inicio de sesión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="933bb-117">Reemplace `clustername` con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="933bb-118"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="933bb-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="933bb-119">Un clúster de Hadoop basado en Linux en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="933bb-120">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="933bb-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="933bb-121">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="933bb-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="933bb-122">Un cliente de SSH o un cliente de Beeline local.</span><span class="sxs-lookup"><span data-stu-id="933bb-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="933bb-123">La mayoría de los pasos de hello en este documento se supone que está usando Beeline desde un clúster de toohello de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="933bb-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="933bb-124">Para obtener información acerca de cómo ejecutar Beeline de clúster fuera de hello, vea hello [usar de forma remota Beeline](#remote) sección.</span><span class="sxs-lookup"><span data-stu-id="933bb-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="933bb-125">Para obtener más información sobre cómo usar SSH, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="933bb-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="933bb-126"><a id="beeline"></a>Uso de BeeLine</span><span class="sxs-lookup"><span data-stu-id="933bb-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="933bb-127">Cuando Beeline se inicia, hay que proporcionar una cadena de conexión de HiveServer2 en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="933bb-128">comando de hello toorun de clúster fuera de hello, debe proporcionar un nombre de cuenta de inicio de sesión de clúster de hello (valor predeterminado `admin`) y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="933bb-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="933bb-129">Usar hello después de la tabla toofind Hola conexión cadena formato y los parámetros toouse:</span><span class="sxs-lookup"><span data-stu-id="933bb-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="933bb-130">Desde dónde se ejecuta Beeline</span><span class="sxs-lookup"><span data-stu-id="933bb-130">Where you run Beeline from</span></span> | <span data-ttu-id="933bb-131">parameters</span><span class="sxs-lookup"><span data-stu-id="933bb-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="933bb-132">Un nodo de nodo principal o de borde del tooa de conexión de SSH</span><span class="sxs-lookup"><span data-stu-id="933bb-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="933bb-133">Clúster de hello exterior</span><span class="sxs-lookup"><span data-stu-id="933bb-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="933bb-134">Por ejemplo, hello siguiente comando puede ser usado toostart Beeline desde un clúster de toohello de sesión SSH:</span><span class="sxs-lookup"><span data-stu-id="933bb-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="933bb-135">Este comando inicia a hello Beeline cliente y conecta tooHiveServer2 en el nodo principal del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="933bb-136">Cuando se completa el comando hello, llega a un `jdbc:hive2://headnodehost:10001/>` símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="933bb-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="933bb-137">Los comandos de Beeline empiezan con un carácter `!`. Por ejemplo `!help` muestra la ayuda.</span><span class="sxs-lookup"><span data-stu-id="933bb-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="933bb-138">Sin embargo Hola `!` puede omitirse en algunos comandos.</span><span class="sxs-lookup"><span data-stu-id="933bb-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="933bb-139">Por ejemplo, `help` también funciona.</span><span class="sxs-lookup"><span data-stu-id="933bb-139">For example, `help` also works.</span></span>

    <span data-ttu-id="933bb-140">Hay un `!sql`, que es usado tooexecute instrucciones de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="933bb-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="933bb-141">Sin embargo, HiveQL es lo más frecuente que puede omitir Hola anterior `!sql`.</span><span class="sxs-lookup"><span data-stu-id="933bb-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="933bb-142">Hola siguiendo dos instrucciones es equivalente:</span><span class="sxs-lookup"><span data-stu-id="933bb-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="933bb-143">En un nuevo clúster, solo debe aparecer una tabla: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="933bb-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="933bb-144">Usar hello después de esquema comando toodisplay Hola Hola hivesampletable:</span><span class="sxs-lookup"><span data-stu-id="933bb-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="933bb-145">Este comando devuelve Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="933bb-145">This command returns hello following information:</span></span>

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

    <span data-ttu-id="933bb-146">Esta información describe las columnas de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="933bb-147">Mientras se pueden llevar a cabo algunas consultas con estos datos, vamos a en su lugar, crear una nueva toodemonstrate tabla cómo datos tooload en Hive y aplicar un esquema.</span><span class="sxs-lookup"><span data-stu-id="933bb-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="933bb-148">Escriba Hola siguiendo las instrucciones toocreate una tabla denominada **log4jLogs** mediante el uso de datos de ejemplo proporcionados con clúster de HDInsight de hello:</span><span class="sxs-lookup"><span data-stu-id="933bb-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="933bb-149">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="933bb-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="933bb-150">`DROP TABLE`-Si existe en la tabla de hello, se elimina.</span><span class="sxs-lookup"><span data-stu-id="933bb-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="933bb-151">`CREATE EXTERNAL TABLE`: crea una tabla **externa** en Hive.</span><span class="sxs-lookup"><span data-stu-id="933bb-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="933bb-152">Tablas externas solo almacenan definición de la tabla de hello en el subárbol.</span><span class="sxs-lookup"><span data-stu-id="933bb-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="933bb-153">Hola datos permanecen en la ubicación original de Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="933bb-154">`ROW FORMAT`-Cómo se da formato a los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="933bb-155">En este caso, los campos de hello en cada registro están separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="933bb-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="933bb-156">`STORED AS TEXTFILE LOCATION`-Donde se almacenan los datos de Hola y en qué formato de archivo.</span><span class="sxs-lookup"><span data-stu-id="933bb-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="933bb-157">`SELECT`-Selecciona un recuento de todas las filas donde columna **t4** contiene el valor de hello **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="933bb-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="933bb-158">Esta consulta devuelve un valor de **3** ya que hay tres filas que contienen este valor.</span><span class="sxs-lookup"><span data-stu-id="933bb-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="933bb-159">`INPUT__FILE__NAME LIKE '%.log'`-Subárbol intenta tooapply Hola esquema tooall archivos hello del directorio.</span><span class="sxs-lookup"><span data-stu-id="933bb-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="933bb-160">En este caso, el directorio de hello contiene archivos que no coinciden con el esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="933bb-161">tooprevent los datos de elementos no utilizados en los resultados de hello, esta instrucción indica Hive que solo debemos devolver datos de archivos que finalizan con. registro.</span><span class="sxs-lookup"><span data-stu-id="933bb-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="933bb-162">Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo.</span><span class="sxs-lookup"><span data-stu-id="933bb-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="933bb-163">Por ejemplo, un proceso de carga de datos automatizado o una operación de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="933bb-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="933bb-164">Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="933bb-165">Hola de salida de este comando es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="933bb-165">hello output of this command is similar toohello following text:</span></span>

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

5. <span data-ttu-id="933bb-166">usar tooexit Beeline, `!exit`.</span><span class="sxs-lookup"><span data-stu-id="933bb-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="933bb-167"><a id="file"></a>Usar Beeline toorun un archivo de HiveQL</span><span class="sxs-lookup"><span data-stu-id="933bb-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="933bb-168">Usar hello siguiendo los pasos toocreate un archivo, a continuación, ejecutarlo mediante Beeline.</span><span class="sxs-lookup"><span data-stu-id="933bb-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="933bb-169">Comando de uso Hola siguiente toocreate un archivo denominado **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="933bb-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="933bb-170">Usar hello después de texto como contenido de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="933bb-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="933bb-171">Esta consulta crea una nueva tabla "interna" denominada **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="933bb-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="933bb-172">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="933bb-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="933bb-173">**Crear tabla IF NOT EXISTS** -si aún no existe la tabla de hello, se crea.</span><span class="sxs-lookup"><span data-stu-id="933bb-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="933bb-174">Desde hello **externo** no se utiliza la palabra clave, esta instrucción crea una tabla interna.</span><span class="sxs-lookup"><span data-stu-id="933bb-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="933bb-175">Las tablas internas se almacenan en el almacén de datos de Hive de Hola y se administran completamente por el subárbol.</span><span class="sxs-lookup"><span data-stu-id="933bb-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="933bb-176">**ALMACENA AS ORC** -almacena los datos de hello en formato optimizado fila columnas (ORC).</span><span class="sxs-lookup"><span data-stu-id="933bb-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="933bb-177">ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="933bb-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="933bb-178">**INSERT OVERWRITE ... Seleccione** -selecciona las filas de hello **log4jLogs** tabla que contenga **[ERROR]**, a continuación, inserta Hola datos en hello **registros de errores de** tabla.</span><span class="sxs-lookup"><span data-stu-id="933bb-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="933bb-179">A diferencia de las tablas externas, al quitar una tabla interna, eliminan datos subyacente de saludo.</span><span class="sxs-lookup"><span data-stu-id="933bb-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="933bb-180">archivo de hello toosave, use **Ctrl**+**_X**, a continuación, escriba **Y**y, finalmente, **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="933bb-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="933bb-181">Usar hello toorun Hola archivo mediante Beeline siguiente:</span><span class="sxs-lookup"><span data-stu-id="933bb-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="933bb-182">Hola `-i` parámetro Beeline inicia, se ejecuta Hola instrucciones en el archivo de hello query.hql.</span><span class="sxs-lookup"><span data-stu-id="933bb-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="933bb-183">Cuando se completa la consulta de hello, llegan hello `jdbc:hive2://headnodehost:10001/>` símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="933bb-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="933bb-184">También puede ejecutar un archivo mediante hello `-f` parámetro, que Beeline se cierra después de completarse Hola consulta.</span><span class="sxs-lookup"><span data-stu-id="933bb-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="933bb-185">tooverify que Hola **registros de errores de** se creó la tabla, use Hola después tooreturn instrucción todos Hola filas de **registros de errores de**:</span><span class="sxs-lookup"><span data-stu-id="933bb-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="933bb-186">Se deben devolver tres filas de datos y todas ellas deben contener **[ERROR]** en la columna t4.</span><span class="sxs-lookup"><span data-stu-id="933bb-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="933bb-187"><a id="remote"></a>Usar Beeline de forma remota</span><span class="sxs-lookup"><span data-stu-id="933bb-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="933bb-188">Si tiene Beeline instalado localmente, o esté utilizándolo a través de una imagen de Docker como [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), debe usar Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="933bb-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="933bb-189">__Cadena de conexión__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="933bb-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="933bb-190">__Nombre de inicio de sesión del clúster__: `-n admin`</span><span class="sxs-lookup"><span data-stu-id="933bb-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="933bb-191">__Contraseña de inicio de sesión del clúster__`-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="933bb-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="933bb-192">Reemplace hello `clustername` en cadena de conexión de hello con nombre Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="933bb-193">Reemplace `admin` con el nombre de Hola de su inicio de sesión de clúster y `password` con la contraseña de hello para el inicio de sesión de clúster.</span><span class="sxs-lookup"><span data-stu-id="933bb-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="933bb-194"><a id="sparksql"></a>Uso de Beeline con Spark</span><span class="sxs-lookup"><span data-stu-id="933bb-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="933bb-195">Spark proporciona su propia implementación de HiveServer2, que a menudo es servidor Thrift de Spark de usan tooas Hola.</span><span class="sxs-lookup"><span data-stu-id="933bb-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="933bb-196">Este servicio utiliza las consultas de tooresolve Spark SQL en lugar de Hive y puede proporcionar un mejor rendimiento en función de la consulta.</span><span class="sxs-lookup"><span data-stu-id="933bb-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="933bb-197">servidor de tooconnect toohello Thrift de Spark de un Spark en clúster de HDInsight, uso del puerto `10002` en lugar de `10001`.</span><span class="sxs-lookup"><span data-stu-id="933bb-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="933bb-198">Por ejemplo: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="933bb-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="933bb-199">servidor Thrift de Spark de Hello es no directamente accesible over Hola internet.</span><span class="sxs-lookup"><span data-stu-id="933bb-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="933bb-200">Solo puede conectarse tooit desde una sesión de SSH o dentro de Hola misma red Virtual de Azure como Hola clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="933bb-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="933bb-201"><a id="summary"></a><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="933bb-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="933bb-202">Para obtener información general de Hive en HDInsight, vea Hola siguiente documento:</span><span class="sxs-lookup"><span data-stu-id="933bb-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="933bb-203">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="933bb-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="933bb-204">Para obtener más información sobre otras maneras de trabajar con Hadoop en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="933bb-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="933bb-205">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="933bb-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="933bb-206">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="933bb-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="933bb-207">Si usas Tez con Hive, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="933bb-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="933bb-208">Usar hello Tez UI en HDInsight basados en Windows</span><span class="sxs-lookup"><span data-stu-id="933bb-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="933bb-209">Usar hello vista Ambari Tez en HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="933bb-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
