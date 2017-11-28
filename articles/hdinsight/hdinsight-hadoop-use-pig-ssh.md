---
title: "Uso de Pig en Hadoop con SSH en un clúster de HDInsight (Azure) | Microsoft Docs"
description: "Aprenda a conectarse a un clúster de Hadoop basado en Linux con SSH y use luego el comando Pig para ejecutar instrucciones de Pig Latin de forma interactiva o como un trabajo por lotes."
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
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="9660e-103">Ejecución de trabajos de Pig en un clúster basado en Linux con el comando Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="9660e-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="9660e-104">Aprenda a ejecutar trabajos de Pig de forma interactiva desde una conexión SSH a su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9660e-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="9660e-105">El lenguaje de programación de Pig Latin le permite describir las transformaciones que se aplican a los datos de entrada para generar el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="9660e-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9660e-106">Para realizar los pasos que se describen en este documento se requiere un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="9660e-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9660e-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="9660e-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9660e-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9660e-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9660e-109"><a id="ssh"></a>Conexión con SSH</span><span class="sxs-lookup"><span data-stu-id="9660e-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="9660e-110">Use SSH para conectarse a su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9660e-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="9660e-111">En el siguiente ejemplo, se conecta con un clúster denominado **myhdinsight** como la cuenta denominada **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="9660e-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="9660e-112">**Si proporcionó una clave de certificado para la autenticación de SSH** , al crear el clúster de HDInsight, es posible que tenga que especificar la ubicación de la clave privada en el sistema cliente.</span><span class="sxs-lookup"><span data-stu-id="9660e-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="9660e-113">**Si proporcionó una contraseña para la autenticación de SSH**, al crear el clúster de HDInsight, indique la contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="9660e-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="9660e-114">Para obtener más información sobre cómo utilizar SSH con HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9660e-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="9660e-115"><a id="pig"></a>Uso del comando Pig</span><span class="sxs-lookup"><span data-stu-id="9660e-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="9660e-116">Una vez conectado, inicie la interfaz de la línea de comandos (CLI) de Pig mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="9660e-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="9660e-117">Después de un momento, debiera ver un símbolo de sistema de `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="9660e-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="9660e-118">Introduzca la siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="9660e-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="9660e-119">Este comando carga el contenido del archivo sample.log en LOGS.</span><span class="sxs-lookup"><span data-stu-id="9660e-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="9660e-120">Puede ver el contenido del archivo mediante la siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="9660e-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="9660e-121">A continuación, transforme los datos aplicando una expresión regular para extraer solo el nivel de registro en cada registro mediante la instrucción siguiente:</span><span class="sxs-lookup"><span data-stu-id="9660e-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="9660e-122">Puede usar **DUMP** para ver los datos después de la transformación.</span><span class="sxs-lookup"><span data-stu-id="9660e-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="9660e-123">En este caso, utilice `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="9660e-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="9660e-124">Continúe aplicando transformaciones mediante las instrucciones de la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="9660e-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="9660e-125">Instrucción de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="9660e-125">Pig Latin statement</span></span> | <span data-ttu-id="9660e-126">Qué hace la instrucción</span><span class="sxs-lookup"><span data-stu-id="9660e-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="9660e-127">Quita las filas que contienen un valor nulo para el nivel de registro y almacena los resultados en `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="9660e-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="9660e-128">Agrupa las filas por nivel de registro y almacena los resultados en `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="9660e-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="9660e-129">Crea un conjunto de datos que contiene cada valor de registro único y cuántas veces se produce.</span><span class="sxs-lookup"><span data-stu-id="9660e-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="9660e-130">El conjunto de datos se almacena en `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="9660e-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="9660e-131">Ordena los niveles de registro por número (descendente) y los almacena en `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="9660e-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="9660e-132">Utilice `DUMP` para ver el resultado de la transformación después de cada paso.</span><span class="sxs-lookup"><span data-stu-id="9660e-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="9660e-133">También puede guardar los resultados de una transformación mediante la instrucción `STORE` .</span><span class="sxs-lookup"><span data-stu-id="9660e-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="9660e-134">Por ejemplo, la siguiente instrucción guarda el valor de `RESULT` en el directorio `/example/data/pigout` en el almacenamiento predeterminado para el clúster:</span><span class="sxs-lookup"><span data-stu-id="9660e-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="9660e-135">Los datos se almacenan en el directorio especificado en los archivos denominados `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="9660e-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="9660e-136">Si el directorio ya existe, recibe un error.</span><span class="sxs-lookup"><span data-stu-id="9660e-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="9660e-137">Para salir del aviso de grunt, escriba la siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="9660e-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="9660e-138">Archivos por lotes de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="9660e-138">Pig Latin batch files</span></span>

<span data-ttu-id="9660e-139">También puede usar el comando de Pig para ejecutar Pig Latin contenido en un archivo.</span><span class="sxs-lookup"><span data-stu-id="9660e-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="9660e-140">Después de salir del símbolo de sistema de Grunt, use el comando siguiente para canalizar STDIN en un archivo denominado `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="9660e-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="9660e-141">Este archivo se crea en el directorio particular para la cuenta de usuario de SSH.</span><span class="sxs-lookup"><span data-stu-id="9660e-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="9660e-142">Escriba o pegue las siguientes líneas y, a continuación, utilice Ctrl+D cuando finalice.</span><span class="sxs-lookup"><span data-stu-id="9660e-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="9660e-143">Utilice el comando siguiente para ejecutar el archivo `pigbatch.pig` mediante el comando de Pig.</span><span class="sxs-lookup"><span data-stu-id="9660e-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="9660e-144">Una vez que finalice el trabajo por lotes, ve el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="9660e-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="9660e-145"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9660e-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9660e-146">Para obtener información general sobre el uso de Pig en HDInsight, consulte los documentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9660e-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="9660e-147">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9660e-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="9660e-148">Para obtener más información sobre otras maneras de trabajar con Hadoop en HDInsight, consulte los documentos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9660e-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="9660e-149">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9660e-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9660e-150">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9660e-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
