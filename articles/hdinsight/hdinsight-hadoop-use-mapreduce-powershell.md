---
title: Uso de MapReduce y PowerShell con Hadoop (Azure HDInsight)| Microsoft Docs
description: "Obtenga información sobre cómo usar PowerShell para ejecutar trabajos de MapReduce de forma remota con Hadoop en HDInsight."
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
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="c4672-103">Ejecución de trabajos de MapReduce con Hadoop en HDInsight con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4672-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="c4672-104">Este documento proporciona un ejemplo de uso de Azure PowerShell para ejecutar un trabajo de MapReduce en un Hadoop de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4672-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="c4672-105"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c4672-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="c4672-106">**Un clúster de HDInsight (Hadoop en HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="c4672-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c4672-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="c4672-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c4672-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c4672-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c4672-109">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c4672-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="c4672-110"><a id="powershell"></a>Ejecución de un trabajo de MapReduce mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4672-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="c4672-111">Azure PowerShell proporciona *cmdlets* que le permiten ejecutar de manera remota trabajos de MapReduce en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4672-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="c4672-112">De manera interna, esto se logra mediante llamadas REST a [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anteriormente llamado Templeton), que se ejecuta en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4672-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="c4672-113">Los siguientes cmdlets se utilizan al ejecutar trabajos de MapReduce en un clúster de HDInsight remoto.</span><span class="sxs-lookup"><span data-stu-id="c4672-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="c4672-114">**Login-AzureRmAccount**: autentica Azure PowerShell en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4672-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="c4672-115">**New-AzureRmHDInsightMapReduceJobDefinition**: crea una nueva *definición de trabajo* usando la información especificada de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="c4672-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="c4672-116">**Start-AzureRmHDInsightJob**: envía la definición del trabajo a HDInsight, inicia el trabajo y devuelve un objeto de *trabajo* que se puede usar para comprobar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c4672-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="c4672-117">**Wait-AzureRmHDInsightJob**: usa el objeto de trabajo para comprobar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c4672-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="c4672-118">Esperará hasta que el trabajo se complete o se supere el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="c4672-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="c4672-119">**Get-AzureRmHDInsightJobOutput**: se usa para recuperar la salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c4672-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="c4672-120">Los pasos siguientes muestran cómo usar estos cmdlets para ejecutar un trabajo en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4672-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="c4672-121">Mediante un editor, guarde el código siguiente como **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c4672-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="c4672-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="c4672-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="c4672-123">Abra un nuevo símbolo del sistema de **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="c4672-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="c4672-124">Cambie los directorios a la ubicación del archivo **mapreducejob.ps1** y, a continuación, utilice el siguiente comando para ejecutar el script:</span><span class="sxs-lookup"><span data-stu-id="c4672-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="c4672-125">Cuando se ejecuta el script, se le pide el nombre del clúster de HDInsight y el nombre de la cuenta de administrador/HTTPS y la contraseña del clúster.</span><span class="sxs-lookup"><span data-stu-id="c4672-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="c4672-126">Puede que también se le pida que autentique su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4672-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="c4672-127">Cuando se complete el trabajo, obtendrá un texto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="c4672-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="c4672-128">Esto indica que el trabajo se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="c4672-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4672-129">Si **ExitCode** es un valor distinto de 0, consulte [Solución de problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="c4672-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="c4672-130">En este ejemplo también se almacenarán los archivos descargados en el archivo **output.txt**, en el directorio desde el que se ejecuta el script.</span><span class="sxs-lookup"><span data-stu-id="c4672-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="c4672-131">Visualización de la salida</span><span class="sxs-lookup"><span data-stu-id="c4672-131">View output</span></span>

<span data-ttu-id="c4672-132">Abra el archivo **output.txt** en un editor de texto para ver las palabras y los números generados por el trabajo.</span><span class="sxs-lookup"><span data-stu-id="c4672-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="c4672-133">Los archivos de salida de un trabajo de MapReduce no se pueden mover.</span><span class="sxs-lookup"><span data-stu-id="c4672-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="c4672-134">Por lo tanto, si vuelve a ejecutar esta muestra, debe cambiar el nombre del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="c4672-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="c4672-135"><a id="troubleshooting"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="c4672-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="c4672-136">Si no se devuelve ninguna información cuando se completa el trabajo, pudo haberse producido un error durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="c4672-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="c4672-137">Para ver información de error para este trabajo, agregue el siguiente comando al final del archivo **mapreducejob.ps1** , guárdelo y luego ejecútelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c4672-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="c4672-138">Este cmdlet devuelve la información escrita en STDERR en el servidor cuando ejecute el trabajo y puede ayudar a determinar por qué se ha producido el error en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="c4672-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="c4672-139"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="c4672-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="c4672-140">Como puede ver, Azure PowerShell proporciona una manera fácil de ejecutar trabajos de MapReduce en un clúster de HDInsight, de supervisar el estado del trabajo y de recuperar el resultado.</span><span class="sxs-lookup"><span data-stu-id="c4672-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="c4672-141"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4672-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c4672-142">Para obtener información general sobre los trabajos de MapReduce en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c4672-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="c4672-143">Uso de MapReduce en Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4672-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c4672-144">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c4672-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c4672-145">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4672-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c4672-146">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4672-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
