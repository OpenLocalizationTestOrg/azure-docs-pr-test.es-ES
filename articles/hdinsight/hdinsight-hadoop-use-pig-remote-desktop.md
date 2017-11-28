---
title: aaaUse Hadoop Pig con Escritorio remoto en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toorun Pig latino instrucciones de Pig comandos desde un clúster de Hadoop basado en Windows de tooa de conexión de escritorio remoto en HDInsight."
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
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="b3817-103">Ejecución de trabajos de Pig desde una conexión de Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="b3817-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="b3817-104">Este documento proporciona un tutorial para utilizar instrucciones de Pig latino Hola Pig comandos toorun desde un clúster de HDInsight basados en Windows de tooa de conexión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="b3817-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="b3817-105">Pig latino permite toocreate MapReduce aplicaciones, se describen las transformaciones de datos, en lugar de asignar y reducir las funciones.</span><span class="sxs-lookup"><span data-stu-id="b3817-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3817-106">Escritorio remoto sólo está disponible en los clústeres de HDInsight que usa Windows como sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3817-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="b3817-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="b3817-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b3817-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b3817-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="b3817-109">Para HDInsight 3.4 o superior, consulte [uso de Pig con HDInsight y SSH](hdinsight-hadoop-use-pig-ssh.md) para obtener información acerca de cómo ejecutar interactivamente Pig trabajos directamente en hello clúster desde una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="b3817-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="b3817-110"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b3817-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="b3817-111">pasos de hello toocomplete en este artículo, deberá siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="b3817-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="b3817-112">Un clúster de HDInsight basado en Windows (Hadoop en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b3817-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="b3817-113">Un equipo cliente con Windows 10, Windows 8 o Windows 7</span><span class="sxs-lookup"><span data-stu-id="b3817-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="b3817-114"><a id="connect"></a>Conexión con el Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="b3817-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="b3817-115">Habilitar Escritorio remoto para el clúster de HDInsight de Hola y conéctela tooit siguiendo las instrucciones de hello en [conectarse mediante RDP de clústeres de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="b3817-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="b3817-116"><a id="pig"></a>Usar comandos de Pig Hola</span><span class="sxs-lookup"><span data-stu-id="b3817-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="b3817-117">Una vez que una conexión a Escritorio remoto, iniciar hello **línea de comandos de Hadoop** mediante el icono de hello en el escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3817-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="b3817-118">Usar hello siguiente toostart Hola Pig comando:</span><span class="sxs-lookup"><span data-stu-id="b3817-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="b3817-119">Aparecerá un símbolo del sistema de `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="b3817-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="b3817-120">Escriba Hola siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="b3817-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="b3817-121">Este comando carga contenido de Hola de archivo sample.log de hello en el archivo de registros de hello.</span><span class="sxs-lookup"><span data-stu-id="b3817-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="b3817-122">Puede ver contenido de Hola de archivo hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b3817-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="b3817-123">Transformar datos de hello aplicando un nivel de registro de hello solo de tooextract de expresión regular de cada registro:</span><span class="sxs-lookup"><span data-stu-id="b3817-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="b3817-124">Puede usar **VOLCAR** datos de hello tooview después de la transformación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3817-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="b3817-125">En este caso, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="b3817-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="b3817-126">Continúe aplicando transformaciones utilizando Hola siguiendo las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="b3817-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="b3817-127">Use `DUMP` tooview resultado de hello de transformación de hello después de cada paso.</span><span class="sxs-lookup"><span data-stu-id="b3817-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="b3817-128">Instrucción</span><span class="sxs-lookup"><span data-stu-id="b3817-128">Statement</span></span></th><th><span data-ttu-id="b3817-129">Qué hace</span><span class="sxs-lookup"><span data-stu-id="b3817-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="b3817-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="b3817-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="b3817-131">Quita las filas que contienen un valor null para el nivel de registro de hello y almacena los resultados de hello en FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="b3817-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="b3817-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="b3817-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="b3817-133">Hola grupos filas por nivel de registro y almacena los resultados de hello en GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="b3817-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="b3817-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="b3817-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="b3817-135">Crea un nuevo conjunto de datos que contiene cada valor de registro único y cuántas veces se produce.</span><span class="sxs-lookup"><span data-stu-id="b3817-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="b3817-136">Esto se almacena en FRECUENCIAS</span><span class="sxs-lookup"><span data-stu-id="b3817-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="b3817-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="b3817-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="b3817-138">Ordena los niveles de registro de hello por recuento (descendente) y almacena en el resultado</span><span class="sxs-lookup"><span data-stu-id="b3817-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="b3817-139">
6.También puede guardar los resultados de Hola de una transformación mediante hello `STORE` instrucción.</span><span class="sxs-lookup"><span data-stu-id="b3817-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="b3817-140">Por ejemplo, hello siguiente comando guarda hello `RESULT` toohello **/example/data/pigout** directorio en el contenedor de almacenamiento predeterminado de hello para el clúster:</span><span class="sxs-lookup"><span data-stu-id="b3817-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="b3817-141">Hola datos se almacenan en el directorio especificado de hello en los archivos denominados **parte nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="b3817-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="b3817-142">Si ya existe el directorio de hello, recibirá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="b3817-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="b3817-143">Hola tooexit grunt símbolo del sistema, escriba Hola después de la instrucción.</span><span class="sxs-lookup"><span data-stu-id="b3817-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="b3817-144">Archivos por lotes de Pig Latin</span><span class="sxs-lookup"><span data-stu-id="b3817-144">Pig Latin batch files</span></span>
<span data-ttu-id="b3817-145">También puede utilizar Hola Pig comando toorun latino Pig que se encuentra en un archivo.</span><span class="sxs-lookup"><span data-stu-id="b3817-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="b3817-146">Después de salir del símbolo del sistema de hello grunt, abra **el Bloc de notas** y crear un nuevo archivo denominado **pigbatch.pig** en hello **PIG_HOME %** directory.</span><span class="sxs-lookup"><span data-stu-id="b3817-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="b3817-147">Tipo o pegar siguiente de hello líneas en hello **pigbatch.pig** de archivos y, a continuación, guárdelo:</span><span class="sxs-lookup"><span data-stu-id="b3817-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="b3817-148">Hola de uso después de hello toorun **pigbatch.pig** archivo mediante el comando de pig Hola.</span><span class="sxs-lookup"><span data-stu-id="b3817-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="b3817-149">Cuando se completa el proceso por lotes de hello, debería ver Hola después de salida, que debe ser igual Hola como cuando usa `DUMP RESULT;` en pasos anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="b3817-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="b3817-150"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="b3817-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="b3817-151">Como puede ver, Hola comando Pig permite toointeractively ejecutar operaciones de MapReduce o ejecutar trabajos de Pig latinos que se almacenan en un archivo por lotes.</span><span class="sxs-lookup"><span data-stu-id="b3817-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="b3817-152"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3817-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="b3817-153">Para obtener información general sobre Pig en HDInsight, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b3817-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="b3817-154">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3817-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="b3817-155">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b3817-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b3817-156">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3817-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b3817-157">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3817-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
