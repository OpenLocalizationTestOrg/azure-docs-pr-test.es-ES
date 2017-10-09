---
title: aaaUse MapReduce y PowerShell con Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse PowerShell tooremotely ejecutar trabajos de MapReduce con Hadoop en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="718f4-103">Ejecución de trabajos de MapReduce con Hadoop en HDInsight con PowerShell</span><span class="sxs-lookup"><span data-stu-id="718f4-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="718f4-104">Este documento proporciona un ejemplo del uso de PowerShell de Azure toorun un trabajo MapReduce en un Hadoop en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="718f4-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="718f4-105"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="718f4-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="718f4-106">**Un clúster de HDInsight (Hadoop en HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="718f4-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="718f4-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="718f4-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="718f4-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="718f4-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="718f4-109">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="718f4-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="718f4-110"><a id="powershell"></a>Ejecución de un trabajo de MapReduce mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="718f4-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="718f4-111">Azure PowerShell ofrece *cmdlets* que le permiten tooremotely ejecutar trabajos de MapReduce en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="718f4-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="718f4-112">Internamente, esto se logra mediante llamadas a REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anteriormente denominados Templeton) se ejecuta en Hola clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="718f4-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="718f4-113">Hello siguientes cmdlets se utilizan al ejecutar los trabajos de MapReduce en un clúster de HDInsight remoto.</span><span class="sxs-lookup"><span data-stu-id="718f4-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="718f4-114">**Inicio de sesión AzureRmAccount**: autentica Azure PowerShell tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="718f4-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="718f4-115">**Nueva AzureRmHDInsightMapReduceJobDefinition**: crea un nuevo *definición de trabajo* mediante el uso de hello especifica información de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="718f4-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="718f4-116">**Start-AzureRmHDInsightJob**: envía tooHDInsight de definición de trabajo de hello, inicia el trabajo de Hola y devuelve un *trabajo* objetos que pueden ser utilizados toocheck Hola estado del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="718f4-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="718f4-117">**Espera AzureRmHDInsightJob**: utiliza el estado del objeto toocheck Hola de hello trabajo del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="718f4-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="718f4-118">Espera hasta que complete el trabajo de Hola o se supera el tiempo de espera de Hola.</span><span class="sxs-lookup"><span data-stu-id="718f4-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="718f4-119">**Get-AzureRmHDInsightJobOutput**: utiliza la salida de hello tooretrieve de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="718f4-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="718f4-120">Hello pasos siguientes demuestran cómo toouse estos toorun cmdlets un trabajo en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="718f4-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="718f4-121">Con el editor, guardar Hola siguiente código como **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="718f4-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="718f4-122">Abra un nuevo símbolo del sistema de **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="718f4-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="718f4-123">Cambiar ubicación de toohello de directorios de hello **mapreducejob.ps1** de archivos, a continuación, usar hello sigue la secuencia de comandos de Hola toorun:</span><span class="sxs-lookup"><span data-stu-id="718f4-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="718f4-124">Al ejecutar el script de Hola, le pediremos nombre Hola Hola del clúster de HDInsight y nombre de la cuenta de hello HTTPS/Admin y la contraseña para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="718f4-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="718f4-125">También es posible que tooauthenticate solicitadas tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="718f4-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="718f4-126">Cuando se completa el trabajo de hello, recibirá toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="718f4-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="718f4-127">Este resultado indica que el trabajo de Hola se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="718f4-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="718f4-128">Si hello **ExitCode** es un valor distinto de 0, vea [solución de problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="718f4-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="718f4-129">En este ejemplo también almacena Hola descargan archivos tooan **output.txt** archivo directorio Hola que ejecutar script de Hola de.</span><span class="sxs-lookup"><span data-stu-id="718f4-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="718f4-130">Visualización de la salida</span><span class="sxs-lookup"><span data-stu-id="718f4-130">View output</span></span>

<span data-ttu-id="718f4-131">Abra hello **output.txt** archivo en un hello toosee de editor de texto es decir y cuenta producido por trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="718f4-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="718f4-132">archivos de salida de Hello de un trabajo de MapReduce son inmutables.</span><span class="sxs-lookup"><span data-stu-id="718f4-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="718f4-133">Por lo que si se vuelve a ejecutar este ejemplo, necesita toochange Hola nombre hello del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="718f4-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="718f4-134"><a id="troubleshooting"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="718f4-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="718f4-135">Si no se devuelve información cuando se completa el trabajo de hello, puede deberse a un error durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="718f4-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="718f4-136">información de error de tooview para este trabajo, agregar Hola siguiente comando toohello final de hello **mapreducejob.ps1** archivo, guárdelo y, a continuación, vuelva a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="718f4-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="718f4-137">Este cmdlet devuelve información de Hola que escribió tooSTDERR en servidor hello cuando ejecutó el trabajo de Hola y puede ayudar a determinar por qué se producen errores en trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="718f4-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="718f4-138"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="718f4-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="718f4-139">Como puede ver, Azure PowerShell ofrece una manera sencilla de toorun trabajos MapReduce en un clúster de HDInsight, supervisar el estado de trabajo de Hola y salida de hello de recuperar.</span><span class="sxs-lookup"><span data-stu-id="718f4-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="718f4-140"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="718f4-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="718f4-141">Para obtener información general sobre los trabajos de MapReduce en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="718f4-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="718f4-142">Uso de MapReduce en Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="718f4-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="718f4-143">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="718f4-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="718f4-144">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="718f4-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="718f4-145">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="718f4-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
