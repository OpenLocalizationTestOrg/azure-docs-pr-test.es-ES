---
title: "aaaUse Hadoop Pig mediante SSH en un clúster de HDInsight - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo conectar tooa basado en Linux, Hadoop clúster mediante SSH y, a continuación, usar Hola Pig comando toorun Pig latino instrucciones interactivamente o como un lote de trabajo."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="9f0d3-103">Ejecutar trabajos de Pig en un clúster basado en Linux con hello comando Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="9f0d3-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="9f0d3-104">Obtenga información acerca de cómo toointeractively ejecutar trabajos de Pig desde un clúster de HDInsight de tooyour de conexión SSH.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="9f0d3-105">Hola lenguaje de programación de Pig latino permite transformaciones toodescribe toohello aplicado entrada datos tooproduce Hola deseado de salida.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f0d3-106">Hello pasos de este documento requieren un clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9f0d3-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9f0d3-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9f0d3-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9f0d3-109"><a id="ssh"></a>Conexión con SSH</span><span class="sxs-lookup"><span data-stu-id="9f0d3-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="9f0d3-110">Use el clúster de HDInsight de tooyour tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="9f0d3-111">Hello en el ejemplo siguiente se conecta con el nombre de clúster de tooa **myhdinsight** como cuenta de hello denominada **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="9f0d3-112">**Si proporciona una clave de certificado para la autenticación de SSH** cuando se creó el clúster de HDInsight de hello, puede que necesite toospecify ubicación de Hola de clave privada de hello en el sistema cliente.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="9f0d3-113">**Si proporciona una contraseña para la autenticación de SSH** cuando se creó el clúster de HDInsight de hello, proporcionar contraseña de hello cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="9f0d3-114">Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9f0d3-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="9f0d3-115"><a id="pig"></a>Usar comandos de Pig Hola</span><span class="sxs-lookup"><span data-stu-id="9f0d3-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="9f0d3-116">Una vez conectado, inicie la interfaz de línea de comandos de Pig hello (CLI) mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="9f0d3-117">Después de un momento, debiera ver un símbolo de sistema de `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="9f0d3-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="9f0d3-118">Escriba Hola siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="9f0d3-119">Este comando carga contenido de Hola de archivo sample.log de hello en los registros.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="9f0d3-120">Puede ver contenido de Hola de archivo hello mediante Hola siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="9f0d3-121">A continuación, transformar datos de hello aplicando un nivel de registro de hello solo de tooextract de expresión regular de cada registro mediante el uso de hello siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="9f0d3-122">Puede usar **VOLCAR** datos de hello tooview después de la transformación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="9f0d3-123">En este caso, utilice `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="9f0d3-124">Continúe aplicando transformaciones mediante instrucciones de hello en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="9f0d3-125">Instrucción de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="9f0d3-125">Pig Latin statement</span></span> | <span data-ttu-id="9f0d3-126">¿Qué instrucción Hola realiza</span><span class="sxs-lookup"><span data-stu-id="9f0d3-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="9f0d3-127">Quita las filas que contienen un valor null para el nivel de registro de hello y almacena los resultados de hello en `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="9f0d3-128">Hola grupos filas por nivel de registro y almacena los resultados de hello en `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="9f0d3-129">Crea un conjunto de datos que contiene cada valor de registro único y cuántas veces se produce.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="9f0d3-130">conjunto de datos de Hola se almacena en `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="9f0d3-131">Ordena los niveles de registro de hello por recuento (descendente) y almacena en `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="9f0d3-132">Use `DUMP` tooview resultado de hello de transformación de hello después de cada paso.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="9f0d3-133">También puede guardar los resultados de Hola de una transformación mediante hello `STORE` instrucción.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="9f0d3-134">Por ejemplo, después de la instrucción de hello guarda hello `RESULT` toohello `/example/data/pigout` directorio de almacenamiento predeterminado de hello para el clúster:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="9f0d3-135">Hola datos se almacenan en el directorio especificado de hello en los archivos denominados `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="9f0d3-136">Si ya existe el directorio de hello, recibirá un error.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="9f0d3-137">Hola tooexit grunt símbolo del sistema, escriba Hola siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="9f0d3-138">Archivos por lotes de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="9f0d3-138">Pig Latin batch files</span></span>

<span data-ttu-id="9f0d3-139">También puede utilizar Hola Pig comando toorun latino Pig contenidos en un archivo.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="9f0d3-140">Después de salir del símbolo del sistema de hello grunt, siguiente Hola de uso del comando toopipe STDIN en un archivo denominado `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="9f0d3-141">Este archivo se crea en el directorio principal Hola Hola cuenta de usuario SSH.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="9f0d3-142">Escriba o pegue Hola siguiendo las líneas y, a continuación, utilice Ctrl + D cuando termine.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="9f0d3-143">Siguiente Hola de uso del comando hello toorun `pigbatch.pig` archivo mediante el comando de Pig Hola.</span><span class="sxs-lookup"><span data-stu-id="9f0d3-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="9f0d3-144">Una vez que finalice el trabajo por lotes de hello, vea Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="9f0d3-145"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f0d3-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9f0d3-146">Para obtener información general sobre Pig en HDInsight, vea Hola siguiente documento:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="9f0d3-147">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f0d3-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="9f0d3-148">Para obtener más información sobre otra maneras de toowork con Hadoop en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="9f0d3-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="9f0d3-149">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f0d3-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9f0d3-150">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f0d3-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
