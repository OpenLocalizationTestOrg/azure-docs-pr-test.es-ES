---
title: ejemplos de hello aaaRun Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Empezar a trabajar con servicio de HDInsight de Azure Hola Hola ejemplos que se proporcionan. Use scripts de PowerShell que ejecutan programas MapReduce en clústeres de datos."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a><span data-ttu-id="b6ef2-104">Ejecución de ejemplos de Hadoop MapReduce en HDInsight basado en Windows</span><span class="sxs-lookup"><span data-stu-id="b6ef2-104">Run Hadoop MapReduce samples in Windows-based HDInsight</span></span>
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="b6ef2-105">Se proporciona un conjunto de muestras toohelp empezar a ejecutar trabajos MapReduce en clústeres de Hadoop con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-105">A set of samples are provided toohelp you get started running MapReduce jobs on Hadoop clusters using Azure HDInsight.</span></span> <span data-ttu-id="b6ef2-106">Estos ejemplos se ponen a disposición de cada uno de hello HDInsight clústeres administrados creados por usted.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-106">These samples are made available on each of hello HDInsight managed clusters that you create.</span></span> <span data-ttu-id="b6ef2-107">Estos ejemplos de la ejecución familiarizarse con el uso de trabajos de toorun de cmdlets de PowerShell de Azure en clústeres de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-107">Running these samples familiarize you with using Azure PowerShell cmdlets toorun jobs on Hadoop clusters.</span></span>

* <span data-ttu-id="b6ef2-108">[**Recuento de palabras**][hdinsight-sample-wordcount]: cuenta las apariciones de una palabra en un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-108">[**Word count**][hdinsight-sample-wordcount]: Counts word occurrences in a text file.</span></span>
* <span data-ttu-id="b6ef2-109">[**Número de palabras de transmisión por secuencias de C#**][hdinsight-sample-csharp-streaming]: Hola de apariciones de recuentos de palabras en un archivo de texto con interfaz de streaming de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-109">[**C# streaming word count**][hdinsight-sample-csharp-streaming]: Counts word occurrences in a text file using hello Hadoop streaming interface.</span></span>
* <span data-ttu-id="b6ef2-110">[**Estimador de PI**][hdinsight-sample-pi-estimator]: utiliza una estadística (tipo de Monte Carlo) valor del método tooestimate Hola de pi.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-110">[**Pi estimator**][hdinsight-sample-pi-estimator]: Uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span>
* <span data-ttu-id="b6ef2-111">[**Graysort de 10 GB**][hdinsight-sample-10gb-graysort]: se ejecuta una muestra de GraySort de uso general en un archivo de 10 GB mediante HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: Run a general-purpose GraySort on a 10 GB file by using HDInsight.</span></span> <span data-ttu-id="b6ef2-112">Hay tres toorun de trabajos: Teragen toogenerate Hola datos, datos de hello toosort Terasort y tooconfirm Teravalidate que se han ordenado correctamente datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-112">There are three jobs toorun: Teragen toogenerate hello data, Terasort toosort hello data, and Teravalidate tooconfirm that hello data has been properly sorted.</span></span>

> [!NOTE]
> <span data-ttu-id="b6ef2-113">código fuente de Hello puede encontrarse en el apéndice de hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-113">hello source code can be found in hello Appendix.</span></span>

<span data-ttu-id="b6ef2-114">Existe documentación adicional mucho en web de Hola para las tecnologías relacionadas con Hadoop, como la programación de MapReduce basados en Java y transmisión por secuencias y documentación acerca de los cmdlets de Hola que se usan en Windows PowerShell scripting.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-114">Much additional documentation exists on hello web for Hadoop-related technologies, such as Java-based MapReduce programming and streaming, and documentation about hello cmdlets that are used in Windows PowerShell scripting.</span></span> <span data-ttu-id="b6ef2-115">Para obtener más información acerca de estos recursos, consulte:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-115">For more information about these resources, see:</span></span>

* [<span data-ttu-id="b6ef2-116">Desarrollo de programas MapReduce de Java para Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ef2-116">Develop Java MapReduce programs for Hadoop in HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [<span data-ttu-id="b6ef2-117">Envío de trabajos de Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ef2-117">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* <span data-ttu-id="b6ef2-118">[Introducción tooAzure HDInsight][hdinsight-introduction]</span><span class="sxs-lookup"><span data-stu-id="b6ef2-118">[Introduction tooAzure HDInsight][hdinsight-introduction]</span></span>

<span data-ttu-id="b6ef2-119">En la actualidad, muchas personas prefieren Hive y Pig a MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-119">Nowadays, many people choose Hive and Pig over MapReduce.</span></span>  <span data-ttu-id="b6ef2-120">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-120">For more information, see:</span></span>

* [<span data-ttu-id="b6ef2-121">Uso de Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ef2-121">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b6ef2-122">Uso de Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6ef2-122">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="b6ef2-123">**Requisitos previos**:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-123">**Prerequisites**:</span></span>

* <span data-ttu-id="b6ef2-124">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-124">**An Azure subscription**.</span></span> <span data-ttu-id="b6ef2-125">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-125">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b6ef2-126">**un clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-126">**an HDInsight cluster**.</span></span> <span data-ttu-id="b6ef2-127">Para obtener instrucciones sobre Hola distintas formas en que se pueden crear clústeres como éstos, vea [Hadoop crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-127">For instructions on hello various ways in which such clusters can be created, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="b6ef2-128">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-128">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b6ef2-129">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y desaparecerá por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-129">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="b6ef2-130">Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-130">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="b6ef2-131">Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-131">Follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b6ef2-132">Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-132">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <span data-ttu-id="b6ef2-133"><a name="hdinsight-sample-wordcount"></a>Recuento de palabras: Java</span><span class="sxs-lookup"><span data-stu-id="b6ef2-133"><a name="hdinsight-sample-wordcount"></a>Word count - Java</span></span>
<span data-ttu-id="b6ef2-134">toosubmit un proyecto de MapReduce, primero cree una definición de trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-134">toosubmit a MapReduce project, you first create a MapReduce job definition.</span></span> <span data-ttu-id="b6ef2-135">En la definición del trabajo hello, especificar archivo jar de hello MapReduce programa y la ubicación de Hola de archivo jar de hello, que es **wasb:///example/jars/hadoop-mapreduce-examples.jar**, Hola nombre de clase y Hola argumentos.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-135">In hello job definition, you specify hello MapReduce program jar file and hello location of hello jar file, which is **wasb:///example/jars/hadoop-mapreduce-examples.jar**, hello class name, and hello arguments.</span></span>  <span data-ttu-id="b6ef2-136">programa de Hello wordcount MapReduce toma dos argumentos: archivo de código fuente de Hola que es usado toocount palabras y la ubicación de hello para la salida.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-136">hello wordcount MapReduce program takes two arguments: hello source file that is used toocount words, and hello location for output.</span></span>

<span data-ttu-id="b6ef2-137">código fuente de Hello puede encontrarse en hello [Apéndice A](#apendix-a---the-word-count-MapReduce-program-in-java).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-137">hello source code can be found in hello [Appendix A](#apendix-a---the-word-count-MapReduce-program-in-java).</span></span>

<span data-ttu-id="b6ef2-138">Procedimiento de Hola de desarrollar un MapReduce de Java, consulte - [programas de MapReduce desarrollar de Java para Hadoop en HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span><span class="sxs-lookup"><span data-stu-id="b6ef2-138">For hello procedure of developing a Java MapReduce program, see - [Develop Java MapReduce programs for Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span></span>

<span data-ttu-id="b6ef2-139">**toosubmit un trabajo de MapReduce de recuento de palabras**</span><span class="sxs-lookup"><span data-stu-id="b6ef2-139">**toosubmit a word count MapReduce job**</span></span>

1. <span data-ttu-id="b6ef2-140">Abra **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-140">Open **Windows PowerShell ISE**.</span></span> <span data-ttu-id="b6ef2-141">Para obtener más información, consulte [Instalación y configuración de Azure PowerShell][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="b6ef2-141">For instructions, see [Install and configure Azure PowerShell][powershell-install-configure].</span></span>
2. <span data-ttu-id="b6ef2-142">Pegue el siguiente script de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-142">Paste hello following PowerShell script:</span></span>

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    <span data-ttu-id="b6ef2-143">trabajo de MapReduce Hello genera un archivo denominado *parte-r-00000*, que contiene palabras y recuentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-143">hello MapReduce job produces a file named *part-r-00000*, which contains words and hello counts.</span></span> <span data-ttu-id="b6ef2-144">script de Hola usa hello **findstr** comando toolist Hola a todas las palabras que contiene *"there"*.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-144">hello script uses hello **findstr** command toolist all hello words that contains *"there"*.</span></span>
3. <span data-ttu-id="b6ef2-145">Establecer hello en primer lugar tres variables y ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-145">Set hello first three variables, and run hello script.</span></span>

## <span data-ttu-id="b6ef2-146"><a name="hdinsight-sample-csharp-streaming"></a>Recuento de palabras: streaming en C#</span><span class="sxs-lookup"><span data-stu-id="b6ef2-146"><a name="hdinsight-sample-csharp-streaming"></a>Word count - C# streaming</span></span>
<span data-ttu-id="b6ef2-147">Hadoop proporciona una transmisión por secuencias tooMapReduce API, lo que permite asignar toowrite así como funciones en lenguajes distintos de Java.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-147">Hadoop provides a streaming API tooMapReduce, which enables you toowrite map and reduce functions in languages other than Java.</span></span>

> [!NOTE]
> <span data-ttu-id="b6ef2-148">pasos de Hello en este tutorial aplican según tooWindows solo clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-148">hello steps in this tutorial apply only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="b6ef2-149">Para obtener un ejemplo de streaming para clústeres de HDInsight basados en Linux, consulte [Desarrollo de programas de streaming en Python para HDInsight](hdinsight-hadoop-streaming-python.md).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-149">For an example of streaming for Linux-based HDInsight clusters, see [Develop Python streaming programs for HDInsight](hdinsight-hadoop-streaming-python.md).</span></span>

<span data-ttu-id="b6ef2-150">En hello (ejemplo), el asignador de Hola y reductor Hola son archivos ejecutables que leen la entrada de Hola de [stdin] [ stdin-stdout-stderr] (línea por línea) y emitir la salida de hello demasiado[stdout] [stdin-stdout-stderr].</span><span class="sxs-lookup"><span data-stu-id="b6ef2-150">In hello example, hello mapper and hello reducer are executables that read hello input from [stdin][stdin-stdout-stderr] (line-by-line) and emit hello output too[stdout][stdin-stdout-stderr].</span></span> <span data-ttu-id="b6ef2-151">programa Hello cuenta todas las palabras de hello en texto hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-151">hello program counts all hello words in hello text.</span></span>

<span data-ttu-id="b6ef2-152">Cuando se especifica un archivo ejecutable para **asignadores**, cada tarea de asignador inicia Hola ejecutable como un proceso independiente cuando se inicializa el asignador de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-152">When an executable is specified for **mappers**, each mapper task launches hello executable as a separate process when hello mapper is initialized.</span></span> <span data-ttu-id="b6ef2-153">Tal y como se ejecuta la tarea de asignador de hello, su entrada convierte en líneas y fuentes Hola líneas toohello [stdin] [ stdin-stdout-stderr] del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-153">As hello mapper task runs, it converts its input into lines, and feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="b6ef2-154">Hola mientras tanto, el asignador de hello recopila salida orientada a líneas de hello de hello stdout del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-154">In hello meantime, hello mapper collects hello line-oriented output from hello stdout of hello process.</span></span> <span data-ttu-id="b6ef2-155">Cada línea convierte en un par de clave/valor, que se recopila como salida de hello de asignador de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-155">It converts each line into a key/value pair, which is collected as hello output of hello mapper.</span></span> <span data-ttu-id="b6ef2-156">De forma predeterminada, prefijo Hola de una línea arriba toohello primer carácter de tabulación es la clave de hello y, resto Hola de línea hello (excepto Hola carácter de tabulación) es el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-156">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span> <span data-ttu-id="b6ef2-157">Si no hay ningún carácter de tabulación en línea hello, toda la línea se considera como clave de Hola y Hola valor es null.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-157">If there is no Tab character in hello line, entire line is considered as hello key, and hello value is null.</span></span>

<span data-ttu-id="b6ef2-158">Cuando se especifica un archivo ejecutable para **reductores**, cada tarea reductor inicia Hola ejecutable como un proceso independiente cuando se inicializa el reductor Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-158">When an executable is specified for **reducers**, each reducer task launches hello executable as a separate process when hello reducer is initialized.</span></span> <span data-ttu-id="b6ef2-159">Hola reductor tarea se ejecuta, sus pares clave-valor de entrada convierte en líneas y fuentes de hello líneas toohello [stdin] [ stdin-stdout-stderr] del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-159">As hello reducer task runs, it converts its input key/values pairs into lines, and it feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="b6ef2-160">Hola mientras tanto, reductor Hola recopila salida orientada a líneas de hello de hello [stdout] [ stdin-stdout-stderr] del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-160">In hello meantime, hello reducer collects hello line-oriented output from hello [stdout][stdin-stdout-stderr] of hello process.</span></span> <span data-ttu-id="b6ef2-161">Convierte a cada par de clave/valor tooa de línea, que se recopila como salida de hello de reductor Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-161">It converts each line tooa key/value pair, which is collected as hello output of hello reducer.</span></span> <span data-ttu-id="b6ef2-162">De forma predeterminada, prefijo Hola de una línea arriba toohello primer carácter de tabulación es la clave de hello y, resto Hola de línea hello (excepto Hola carácter de tabulación) es el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-162">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span>

<span data-ttu-id="b6ef2-163">**trabajo de recuento de palabras streaming toosubmit C#**</span><span class="sxs-lookup"><span data-stu-id="b6ef2-163">**toosubmit a C# streaming word count job**</span></span>

* <span data-ttu-id="b6ef2-164">Siga el procedimiento de hello en [contar - Java palabras](#word-count-java)y reemplace la definición de trabajo de hello con hello después de línea:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-164">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    <span data-ttu-id="b6ef2-165">archivo de salida de Hello será:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-165">hello output file shall be:</span></span>

        example/data/StreamingOutput/wc.txt/part-00000

## <span data-ttu-id="b6ef2-166"><a name="hdinsight-sample-pi-estimator"></a>Estimador de pi</span><span class="sxs-lookup"><span data-stu-id="b6ef2-166"><a name="hdinsight-sample-pi-estimator"></a>PI estimator</span></span>
<span data-ttu-id="b6ef2-167">Estimador de pi Hello usa una estadística (tipo de Monte Carlo) valor del método tooestimate Hola de pi.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-167">hello pi estimator uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="b6ef2-168">Puntos colocados aleatoriamente dentro de una unidad cuadrado también se sitúan dentro de un círculo inscribe dentro de ese cuadrado con un área de toohello igual de probabilidad del círculo hello, pi/4.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-168">Points placed at random inside of a unit square also fall within a circle inscribed within that square with a probability equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="b6ef2-169">valor de Hola de pi se puede estimar de valor de Hola de 4R, donde R es la proporción de hello del número de Hola de puntos que están dentro de círculo hello toohello número total de puntos que están dentro de cuadrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-169">hello value of pi can be estimated from hello value of 4R, where R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="b6ef2-170">Hola Hola muestra de mayor tamaño puntos usados, que es mejor estimación de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-170">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="b6ef2-171">script de Hola proporcionado para este ejemplo envía un trabajo de Hadoop jar y está configurado toorun con un valor de 16 mapas, cada uno de los cuales es toocompute requiere 10 millones de puntos de ejemplo por valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-171">hello script provided for this sample submits a Hadoop jar job and is set up toorun with a value 16 maps, each of which is required toocompute 10 million sample points by hello parameter values.</span></span> <span data-ttu-id="b6ef2-172">Estos parámetros los valores pueden cambiar tooimprove Hola estimado valor de pi.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-172">These parameter values can be changed tooimprove hello estimated value of pi.</span></span> <span data-ttu-id="b6ef2-173">Como referencia, hello 10 primeros decimales de pi son 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-173">For reference, hello first 10 decimal places of pi are 3.1415926535.</span></span>

<span data-ttu-id="b6ef2-174">**toosubmit un trabajo del estimador de pi**</span><span class="sxs-lookup"><span data-stu-id="b6ef2-174">**toosubmit a pi estimator job**</span></span>

* <span data-ttu-id="b6ef2-175">Siga el procedimiento de hello en [contar - Java palabras](#word-count-java)y reemplace la definición de trabajo de hello con hello después de línea:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-175">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <span data-ttu-id="b6ef2-176"><a name="hdinsight-sample-10gb-graysort"></a>GraySort de 10 GB</span><span class="sxs-lookup"><span data-stu-id="b6ef2-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span></span>
<span data-ttu-id="b6ef2-177">Este ejemplo utiliza solo 10 GB de datos, para así poder ejecutarlo relativamente rápido.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-177">This sample uses a modest 10GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="b6ef2-178">Usa las aplicaciones de MapReduce Hola desarrolladas por Owen O'Malley y Arun Murthy lograda comparativa de ordenación de hello anual uso general ("daytona") terabyte en 2009 con una velocidad de 0.578 TB/min (100 TB en 173 minutos).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-178">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy that won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578TB/min (100TB in 173 minutes).</span></span> <span data-ttu-id="b6ef2-179">Para obtener más información sobre este y otros criterios de ordenación de referencia, vea hello [Sortbenchmark](http://sortbenchmark.org/) sitio.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-179">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="b6ef2-180">Este ejemplo utiliza tres conjuntos de programas de MapReduce:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-180">This sample uses three sets of MapReduce programs:</span></span>

1. <span data-ttu-id="b6ef2-181">**TeraGen** es un programa de MapReduce que se pueden usar filas de hello toogenerate de toosort de datos.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-181">**TeraGen** is a MapReduce program that you can use toogenerate hello rows of data toosort.</span></span>
2. <span data-ttu-id="b6ef2-182">**TeraSort** muestrea los datos de entrada de Hola y utiliza datos de hello toosort MapReduce en un orden total.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-182">**TeraSort** samples hello input data and uses MapReduce toosort hello data into a total order.</span></span> <span data-ttu-id="b6ef2-183">TeraSort es una ordenación estándar de funciones de MapReduce, excepto un particionador personalizado que utiliza una lista ordenada de claves de n-1 muestreada que definen el intervalo de claves de Hola para cada reduce.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-183">TeraSort is a standard sort of MapReduce functions, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="b6ef2-184">En particular, todas las claves de este tipo que muestra [i-1] < = clave < [i] de ejemplo se envían tooreduce.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-184">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="b6ef2-185">Esto garantiza que las salidas de Hola de reducen i es todos los menores de reducir la salida de hello de i + 1.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-185">This guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>
3. <span data-ttu-id="b6ef2-186">**TeraValidate** es un programa de MapReduce que valida que los resultados del Hola global está ordenado.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-186">**TeraValidate** is a MapReduce program that validates that hello output is globally sorted.</span></span> <span data-ttu-id="b6ef2-187">Crea una asignación por cada archivo en el directorio de salida de hello, y cada asignación garantiza que cada clave es menor o igual toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-187">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="b6ef2-188">función de asignación de Hello también genera registros de hello primero y último claves de cada archivo y Hola reducen (función) garantiza que Hola primera clave de archivo i es mayor que la clave de la última Hola de i-1 de archivo.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-188">hello map function also generates records of hello first and last keys of each file, and hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="b6ef2-189">Los problemas se notifican como una salida de hello reducir con claves de Hola que no están ordenadas.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-189">Any problems are reported as an output of hello reduce with hello keys that are out of order.</span></span>

<span data-ttu-id="b6ef2-190">Hola de entrada y el formato de salida, utilizado por todas las aplicaciones de tres, lee y escribe archivos de texto hello en el formato correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-190">hello input and output format, used by all three applications, reads and writes hello text files in hello right format.</span></span> <span data-ttu-id="b6ef2-191">reducir la salida de Hello de hello replicación estableció too1, en lugar de hello valor predeterminado es 3, porque el contexto de la prueba comparativa de hello no requiere que los datos de salida de hello replicarse en nodos de toomultiple.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-191">hello output of hello reduce has replication set too1, instead of hello default 3, because hello benchmark contest does not require that hello output data be replicated on toomultiple nodes.</span></span>

<span data-ttu-id="b6ef2-192">Ejemplo de Hola, cada tooone correspondiente de programas de MapReduce Hola que se describe en la introducción de Hola se requieren tres tareas:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-192">Three tasks are required by hello sample, each corresponding tooone of hello MapReduce programs described in hello introduction:</span></span>

1. <span data-ttu-id="b6ef2-193">Generar datos de hello para la ordenación mediante la ejecución de hello **TeraGen** trabajo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-193">Generate hello data for sorting by running hello **TeraGen** MapReduce job.</span></span>
2. <span data-ttu-id="b6ef2-194">Ordenar los datos de hello ejecutando hello **TeraSort** trabajo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-194">Sort hello data by running hello **TeraSort** MapReduce job.</span></span>
3. <span data-ttu-id="b6ef2-195">Confirme que los datos de Hola se han ordenado correctamente mediante la ejecución de hello **TeraValidate** trabajo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-195">Confirm that hello data has been correctly sorted by running hello **TeraValidate** MapReduce job.</span></span>

<span data-ttu-id="b6ef2-196">**trabajos de hello toosubmit**</span><span class="sxs-lookup"><span data-stu-id="b6ef2-196">**toosubmit hello jobs**</span></span>

* <span data-ttu-id="b6ef2-197">Siga el procedimiento de hello en [contar - Java palabras](#word-count-java), y use Hola siguiendo las definiciones de trabajos:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-197">Follow hello procedure in [Word count - Java](#word-count-java), and use hello following job definitions:</span></span>

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a><span data-ttu-id="b6ef2-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6ef2-198">Next steps</span></span>
<span data-ttu-id="b6ef2-199">De este artículo y los artículos de hello en cada uno de los ejemplos de hello, ha aprendido cómo las muestras de hello toorun incluyan con hello clústeres de HDInsight mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-199">From this article and hello articles in each of hello samples, you learned how toorun hello samples included with hello HDInsight clusters by using Azure PowerShell.</span></span> <span data-ttu-id="b6ef2-200">Para ver los tutoriales sobre el uso de Pig, Hive y MapReduce con HDInsight, vea Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="b6ef2-200">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="b6ef2-201">[Empezar a trabajar con Hadoop Hive en el uso de auriculares móviles de tooanalyze de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b6ef2-201">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="b6ef2-202">[Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b6ef2-202">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="b6ef2-203">[Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b6ef2-203">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="b6ef2-204">[Envío de trabajos de Hadoop en HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="b6ef2-204">[Submit Hadoop Jobs in HDInsight][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="b6ef2-205">[Documentación de SDK de HDInsight de Azure][hdinsight-sdk-documentation]</span><span class="sxs-lookup"><span data-stu-id="b6ef2-205">[Azure HDInsight SDK documentation][hdinsight-sdk-documentation]</span></span>

## <a name="appendix-a---hello-word-count-source-code"></a><span data-ttu-id="b6ef2-206">Apéndice A - Hola código fuente de recuento de palabras</span><span class="sxs-lookup"><span data-stu-id="b6ef2-206">Appendix A - hello Word count source code</span></span>

```java
package org.apache.hadoop.examples;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
    extends Mapper<Object, Text, Text, IntWritable>{

private final static IntWritable one = new IntWritable(1);
private Text word = new Text();

public void map(Object key, Text value, Context context
                ) throws IOException, InterruptedException {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
    word.set(itr.nextToken());
    context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
    extends Reducer<Text,IntWritable,Text,IntWritable> {
private IntWritable result = new IntWritable();

public void reduce(Text key, Iterable<IntWritable> values,
                    Context context
                    ) throws IOException, InterruptedException {
    int sum = 0;
    for (IntWritable val : values) {
    sum += val.get();
    }
    result.set(sum);
    context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
Configuration conf = new Configuration();
String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
if (otherArgs.length != 2) {
    System.err.println("Usage: wordcount <in> <out>");
    System.exit(2);
    }
Job job = new Job(conf, "word count");
job.setJarByClass(WordCount.class);
job.setMapperClass(TokenizerMapper.class);
job.setCombinerClass(IntSumReducer.class);
job.setReducerClass(IntSumReducer.class);
job.setOutputKeyClass(Text.class);
job.setOutputValueClass(IntWritable.class);
FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
    }
```

## <a name="appendix-b---hello-word-count-streaming-source-code"></a><span data-ttu-id="b6ef2-207">Apéndice B - número de palabras de hello transmisión por secuencias de código fuente</span><span class="sxs-lookup"><span data-stu-id="b6ef2-207">Appendix B - hello word count streaming source code</span></span>
<span data-ttu-id="b6ef2-208">programa de MapReduce Hello usa la aplicación de cat.exe Hola como un texto de asignación interfaz toostream hello en la consola de Hola y Hola wc.exe como Hola reducir el número de hello toocount de interfaz de palabras que se transmiten desde un documento.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-208">hello MapReduce program uses hello cat.exe application as a mapping interface toostream hello text into hello console and hello wc.exe application as hello reduce interface toocount hello number of words that are streamed from a document.</span></span> <span data-ttu-id="b6ef2-209">El asignador de Hola y reductor leen caracteres, línea por línea del flujo de entrada estándar (stdin) de Hola y escribir toohello flujo de salida estándar (stdout).</span><span class="sxs-lookup"><span data-stu-id="b6ef2-209">Both hello mapper and reducer read characters, line-by-line, from hello standard input stream (stdin) and write toohello standard output stream (stdout).</span></span>

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

<span data-ttu-id="b6ef2-210">Hola código asignador en hello cat.cs archivos utiliza una [StreamReader] [ streamreader] tooread caracteres de Hola de Hola entrantes flujo toohello consola, que escribirá Hola flujo de salida estándar de toohello de flujo de objeto con hello estático [Console.Writeline] [ console-writeline] método.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-210">hello mapper code in hello cat.cs file uses a [StreamReader][streamreader] object tooread hello characters of hello incoming stream toohello console, which then writes hello stream toohello standard output stream with hello static [Console.Writeline][console-writeline] method.</span></span>

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

<span data-ttu-id="b6ef2-211">Hola código reductor en hello wc.cs archivos utiliza una [StreamReader] [ streamreader] objeto tooread caracteres Hola flujo de entrada estándar que se han resultado por el asignador de cat.exe Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-211">hello reducer code in hello wc.cs file uses a [StreamReader][streamreader]   object tooread characters from hello standard input stream that have been output by hello cat.exe mapper.</span></span> <span data-ttu-id="b6ef2-212">Tal y como lee los caracteres de hello con hello [Console.Writeline] [ console-writeline] método, recuentos palabras hello contando espacios y caracteres de fin de línea al final de Hola de cada palabra.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-212">As it reads hello characters with hello [Console.Writeline][console-writeline] method, it counts hello words by counting spaces and end-of-line characters at hello end of each word.</span></span> <span data-ttu-id="b6ef2-213">A continuación, escribe flujo de salida estándar de hello toohello total con hello [Console.Writeline] [ console-writeline] método.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-213">It then writes hello total toohello standard output stream with hello [Console.Writeline][console-writeline] method.</span></span>

## <a name="appendix-c---hello-pi-estimator-source-code"></a><span data-ttu-id="b6ef2-214">Apéndice C - Hola código fuente de Pi Estimador</span><span class="sxs-lookup"><span data-stu-id="b6ef2-214">Appendix C - hello Pi estimator source code</span></span>
<span data-ttu-id="b6ef2-215">Estimador de pi Hola código Java que contiene funciones de asignador y reductor Hola está disponible para su inspección siguiente.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-215">hello pi estimator Java code that contains hello mapper and reducer functions is available for inspection below.</span></span> <span data-ttu-id="b6ef2-216">programa de asignador de Hello genera un número especificado de puntos colocado aleatoriamente dentro de un cuadrado de unidad y, a continuación, cuenta número de Hola de esos puntos que están dentro de círculo Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-216">hello mapper program generates a specified number of points placed at random inside of a unit square and then counts hello number of those points that are inside hello circle.</span></span> <span data-ttu-id="b6ef2-217">programa de reductor de Hello acumula puntos contados asignadores de Hola y a continuación, calcula el valor de Hola de pi de hello fórmulas 4R, donde R es la proporción de hello del número de Hola de puntos cuenta dentro de círculo hello toohello número total de puntos que están dentro de cuadrado Hola.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-217">hello reducer program accumulates points counted by hello mappers and then estimates hello value of pi from hello formula 4R, where R is hello ratio of hello number of points counted inside hello circle toohello total number of points that are within hello square.</span></span>

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a><span data-ttu-id="b6ef2-218">Apéndice D - código fuente de hello de 10 gb graysort</span><span class="sxs-lookup"><span data-stu-id="b6ef2-218">Appendix D - hello 10gb graysort source code</span></span>
<span data-ttu-id="b6ef2-219">código de Hello de hello TeraSort MapReduce programa se presenta para la inspección en esta sección.</span><span class="sxs-lookup"><span data-stu-id="b6ef2-219">hello code for hello TeraSort MapReduce program is presented for inspection in this section.</span></span>

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
