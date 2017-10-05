---
title: Uso de Pig en Hadoop con PowerShell en HDInsight (Azure) | Microsoft Docs
description: "Aprenda a enviar trabajos de Pig a un clúster de Hadoop en HDInsight mediante Azure PowerShell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="f306a-103">Uso de Azure PowerShell para ejecutar trabajos de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f306a-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="f306a-104">Este documento proporciona un ejemplo de uso de Azure PowerShell para enviar trabajos de Pig a un clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f306a-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="f306a-105">Pig permite escribir trabajos de MapReduce mediante un lenguaje (Pig Latin) que modela las transformaciones de datos, en lugar de asignar y reducir las funciones.</span><span class="sxs-lookup"><span data-stu-id="f306a-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="f306a-106">Este documento no ofrece una descripción detallada de cómo funcionan las instrucciones de Pig Latin que se usan en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="f306a-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="f306a-107">Para obtener información sobre Pig Latin utilizado en este ejemplo, consulte [Uso de Hive con Hadoop en HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="f306a-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="f306a-108"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f306a-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="f306a-109">**Un clúster de Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f306a-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f306a-110">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="f306a-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f306a-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f306a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="f306a-112">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f306a-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="f306a-113"><a id="powershell"></a>Ejecución de trabajos de Pig mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="f306a-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="f306a-114">Azure PowerShell proporciona *cmdlets* que le permiten ejecutar de manera remota trabajos de Pig en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f306a-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="f306a-115">Internamente, PowerShell realiza llamadas de REST a la instancia de [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) que se ejecuta en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f306a-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="f306a-116">Los cmdlets siguientes se utilizan cuando se ejecutan trabajos de Pig en un clúster de HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="f306a-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="f306a-117">**Login-AzureRmAccount**: autentica Azure PowerShell en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f306a-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="f306a-118">**New-AzureRmHDInsightPigJobDefinition**: crea una *definición de trabajo* con las instrucciones de Pig Latin especificadas.</span><span class="sxs-lookup"><span data-stu-id="f306a-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="f306a-119">**Start-AzureRmHDInsightJob**: envía la definición del trabajo a HDInsight, inicia el trabajo y devuelve un objeto de *trabajo* que se puede usar para comprobar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f306a-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="f306a-120">**Wait-AzureRmHDInsightJob**: usa el objeto de trabajo para comprobar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f306a-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="f306a-121">Esperará hasta que el trabajo se haya completado o haya superado el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="f306a-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="f306a-122">**Get-AzureRmHDInsightJobOutput**: se usa para recuperar la salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f306a-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="f306a-123">Los pasos siguientes muestran cómo usar estos cmdlets para ejecutar un trabajo en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f306a-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="f306a-124">Mediante un editor, guarde el código siguiente como **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="f306a-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="f306a-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="f306a-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="f306a-126">Abra un nuevo símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f306a-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="f306a-127">Cambie los directorios a la ubicación del archivo **pigjob.ps1** y, a continuación, utilice el siguiente comando para ejecutar el script:</span><span class="sxs-lookup"><span data-stu-id="f306a-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="f306a-128">Se le indica que inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f306a-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="f306a-129">Luego, se le pedirá que proporcione el nombre de cuenta y la contraseña de HTTPS/Admin para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f306a-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="f306a-130">Cuando el trabajo se complete, debe devolver información de manera similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="f306a-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="f306a-131"><a id="troubleshooting"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f306a-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="f306a-132">Si no se devuelve ninguna información cuando se completa el trabajo, pudo haberse producido un error durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="f306a-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="f306a-133">Para ver la información de error para este trabajo, agregue lo siguiente al final del archivo **pigjob.ps1** , guárdelo y, a continuación, ejecútelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="f306a-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="f306a-134">Se devuelve la información escrita en STDERR en el servidor cuando ejecute el trabajo y puede ayudar a determinar por qué se ha producido el error en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="f306a-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="f306a-135"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="f306a-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="f306a-136">Como puede ver, Azure PowerShell proporciona una manera fácil de ejecutar trabajos de Pig en un clúster de HDInsight, de supervisar el estado del trabajo y de recuperar el resultado.</span><span class="sxs-lookup"><span data-stu-id="f306a-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="f306a-137"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f306a-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="f306a-138">Para obtener información general sobre Pig en HDInsight, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f306a-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="f306a-139">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f306a-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="f306a-140">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f306a-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f306a-141">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f306a-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f306a-142">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f306a-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
