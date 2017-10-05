---
title: Uso de Pig en Hadoop con Escritorio remoto en HDInsight - Azure | Microsoft Docs
description: "Aprenda a utilizar el comando Pig para ejecutar instrucciones de Pig Latin desde una conexión de Escritorio remoto a un clúster de HDInsight basado en Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="54af2-103">Ejecución de trabajos de Pig desde una conexión de Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="54af2-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="54af2-104">Este documento ofrece un tutorial para que usar el comando Pig para ejecutar instrucciones de Pig Latin desde una conexión de Escritorio remoto a un clúster de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="54af2-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="54af2-105">Pig Latin le permite crear aplicaciones de MapReduce que describen las transformaciones de datos, en lugar de asignar y reducir las funciones.</span><span class="sxs-lookup"><span data-stu-id="54af2-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54af2-106">Remote Desktop solo está disponible para clústeres de HDInsight que usan Windows como sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="54af2-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="54af2-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="54af2-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="54af2-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="54af2-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="54af2-109">Para HDInsight 3.4 o superior, consulte [Uso de Pig con HDInsight y SSH](hdinsight-hadoop-use-pig-ssh.md) para más información sobre cómo ejecutar trabajos de Pig directamente en el clúster desde una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="54af2-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="54af2-110"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="54af2-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="54af2-111">Necesitará lo siguiente para completar los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="54af2-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="54af2-112">Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="54af2-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="54af2-113">Un equipo cliente con Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="54af2-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="54af2-114"><a id="connect"></a>Conexión con el Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="54af2-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="54af2-115">Habilite el Escritorio remoto para el clúster de HDInsight y conéctese a él siguiendo las instrucciones dadas en [Conexión a los clústeres de HDInsight con RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="54af2-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="54af2-116"><a id="pig"></a>Uso del comando Pig</span><span class="sxs-lookup"><span data-stu-id="54af2-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="54af2-117">Desde la sesión de Escritorio remoto, use el icono de **línea de comandos de Hadoop** del escritorio para iniciar la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="54af2-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="54af2-118">Use lo siguiente para iniciar el comando Pig:</span><span class="sxs-lookup"><span data-stu-id="54af2-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="54af2-119">Aparecerá un símbolo del sistema de `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="54af2-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="54af2-120">Introduzca la siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="54af2-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="54af2-121">Este comando carga el contenido del archivo sample.log en LOGS.</span><span class="sxs-lookup"><span data-stu-id="54af2-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="54af2-122">Puede ver el contenido del archivo mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="54af2-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="54af2-123">Transforme los datos aplicando una expresión regular para extraer solo el nivel de registro en cada registro mediante lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="54af2-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="54af2-124">Puede usar **DUMP** para ver los datos después de la transformación.</span><span class="sxs-lookup"><span data-stu-id="54af2-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="54af2-125">En este caso, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="54af2-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="54af2-126">Continúe aplicando transformaciones mediante las instrucciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="54af2-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="54af2-127">Utilice `DUMP` para ver el resultado de la transformación después de cada paso.</span><span class="sxs-lookup"><span data-stu-id="54af2-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="54af2-128">Instrucción</span><span class="sxs-lookup"><span data-stu-id="54af2-128">Statement</span></span></th><th><span data-ttu-id="54af2-129">Qué hace</span><span class="sxs-lookup"><span data-stu-id="54af2-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="54af2-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="54af2-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="54af2-131">Quita las filas que contienen un valor nulo para el nivel de registro y almacena los resultados en FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="54af2-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="54af2-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="54af2-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="54af2-133">Agrupa las filas por nivel de registro y almacena los resultados en GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="54af2-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="54af2-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="54af2-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="54af2-135">Crea un nuevo conjunto de datos que contiene cada valor de registro único y cuántas veces se produce.</span><span class="sxs-lookup"><span data-stu-id="54af2-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="54af2-136">Esto se almacena en FRECUENCIAS</span><span class="sxs-lookup"><span data-stu-id="54af2-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="54af2-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="54af2-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="54af2-138">Ordena los niveles de registro por número (descendente) y los almacena en el resultado (RESULT)</span><span class="sxs-lookup"><span data-stu-id="54af2-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="54af2-139">
6. También puede guardar los resultados de una transformación mediante la instrucción `STORE`.</span><span class="sxs-lookup"><span data-stu-id="54af2-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="54af2-140">Por ejemplo, el siguiente comando guarda el valor `RESULT` en el directorio **/example/data/pigout** en el contenedor de almacenamiento predeterminado para el clúster:</span><span class="sxs-lookup"><span data-stu-id="54af2-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="54af2-141">Los datos se almacenan en el directorio especificado en los archivos denominados **part-nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="54af2-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="54af2-142">Si el directorio ya existe, recibirá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="54af2-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="54af2-143">Para salir del aviso de grunt, introduzca la siguiente instrucción.</span><span class="sxs-lookup"><span data-stu-id="54af2-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="54af2-144">Archivos por lotes de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="54af2-144">Pig Latin batch files</span></span>
<span data-ttu-id="54af2-145">También puede usar el comando de Pig para ejecutar Pig Latin contenido en un archivo.</span><span class="sxs-lookup"><span data-stu-id="54af2-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="54af2-146">Después de salir del aviso de grunt, abra el **Bloc de notas** y cree un nuevo archivo denominado **pigbatch.pig** en el directorio **%PIG_HOME%**.</span><span class="sxs-lookup"><span data-stu-id="54af2-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="54af2-147">Escriba o pegue las siguientes líneas en el archivo **pigbatch.pig** y luego guárdelo cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="54af2-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="54af2-148">Utilice lo siguiente para ejecutar el archivo **pigbatch.pig** mediante el comando de Pig.</span><span class="sxs-lookup"><span data-stu-id="54af2-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="54af2-149">Una vez completado el trabajo por lotes, debería ver el siguiente resultado, que debe ser el mismo que cuando ha utilizado `DUMP RESULT;` en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="54af2-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="54af2-150"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="54af2-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="54af2-151">Como puede ver, el comando de Pig permite ejecutar interactivamente operaciones de MapReduce mediante Pig Latin, así como ejecutar trabajos de Pig Latin almacenados en un archivo por lotes.</span><span class="sxs-lookup"><span data-stu-id="54af2-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="54af2-152"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54af2-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="54af2-153">Para obtener información general sobre Pig en HDInsight, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="54af2-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="54af2-154">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="54af2-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="54af2-155">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="54af2-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="54af2-156">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="54af2-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="54af2-157">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="54af2-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
