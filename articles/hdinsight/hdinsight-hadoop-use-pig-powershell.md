---
title: aaaUse Hadoop Pig con PowerShell en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo agrupar toosubmit Pig trabajos tooa Hadoop en HDInsight con Azure PowerShell."
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
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="34253-103">Utilice trabajos de Pig de Azure PowerShell toorun con HDInsight</span><span class="sxs-lookup"><span data-stu-id="34253-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="34253-104">Este documento proporciona un ejemplo del uso de PowerShell de Azure toosubmit Pig trabajos tooa Hadoop en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34253-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="34253-105">Pig permite toowrite MapReduce trabajos mediante el lenguaje (Pig latino) que modela las transformaciones de datos, en lugar de asignar y reducir las funciones.</span><span class="sxs-lookup"><span data-stu-id="34253-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="34253-106">Este documento no proporciona una descripción detallada de lo que las instrucciones de Pig latino Hola usadas en ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="34253-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="34253-107">Para obtener información acerca de hello latino Pig utilizado en este ejemplo, vea [uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="34253-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="34253-108"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="34253-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="34253-109">**Un clúster de Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="34253-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="34253-110">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="34253-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="34253-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="34253-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="34253-112">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="34253-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="34253-113"><a id="powershell"></a>Ejecución de trabajos de Pig mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="34253-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="34253-114">Azure PowerShell ofrece *cmdlets* que le permiten tooremotely ejecutar trabajos de Pig en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34253-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="34253-115">Internamente, PowerShell usa llamadas REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) con clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="34253-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="34253-116">Hello siguientes cmdlets se utilizan al ejecutar los trabajos de Pig en un clúster de HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="34253-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="34253-117">**Inicio de sesión AzureRmAccount**: autentica Azure PowerShell tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="34253-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="34253-118">**Nueva AzureRmHDInsightPigJobDefinition**: crea un *definición de trabajo* mediante el uso de hello especifica instrucciones de Pig latino</span><span class="sxs-lookup"><span data-stu-id="34253-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="34253-119">**Start-AzureRmHDInsightJob**: envía tooHDInsight de definición de trabajo de hello, inicia el trabajo de Hola y devuelve un *trabajo* objetos que pueden ser utilizados toocheck Hola estado del trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="34253-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="34253-120">**Espera AzureRmHDInsightJob**: utiliza el estado del objeto toocheck Hola de hello trabajo del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="34253-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="34253-121">Espera hasta que se haya completado el trabajo de hello, o se ha superado el tiempo de espera de Hola.</span><span class="sxs-lookup"><span data-stu-id="34253-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="34253-122">**Get-AzureRmHDInsightJobOutput**: utiliza la salida de hello tooretrieve de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="34253-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="34253-123">Hello pasos siguientes demuestran cómo toouse estos toorun cmdlets un trabajo en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34253-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="34253-124">Con el editor, guardar Hola siguiente código como **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="34253-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="34253-125">Abra un nuevo símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34253-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="34253-126">Cambiar ubicación de toohello de directorios de hello **pigjob.ps1** de archivos, a continuación, usar hello sigue la secuencia de comandos de Hola toorun:</span><span class="sxs-lookup"><span data-stu-id="34253-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="34253-127">Son toolog solicitada en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="34253-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="34253-128">A continuación, se le pedirán Hola HTTPs/Admin nombre y la contraseña para el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="34253-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="34253-129">Cuando se completa el trabajo de hello, debe devolver información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="34253-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="34253-130"><a id="troubleshooting"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="34253-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="34253-131">Si no se devuelve información cuando se completa el trabajo de hello, puede deberse a un error durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="34253-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="34253-132">información de error de tooview para este trabajo, agregar Hola siguiente comando toohello final de hello **pigjob.ps1** archivo, guárdelo y, a continuación, vuelva a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="34253-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="34253-133">Devuelve información de Hola que escribió tooSTDERR en servidor hello cuando ejecutó el trabajo de Hola y puede ayudar a determinar por qué se producen errores en trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="34253-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="34253-134"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="34253-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="34253-135">Como puede ver, Azure PowerShell ofrece una manera sencilla de toorun trabajos de Pig en un clúster de HDInsight, supervisar el estado de trabajo de Hola y salida de hello de recuperar.</span><span class="sxs-lookup"><span data-stu-id="34253-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="34253-136"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34253-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="34253-137">Para obtener información general sobre Pig en HDInsight, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="34253-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="34253-138">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="34253-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="34253-139">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="34253-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="34253-140">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="34253-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="34253-141">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="34253-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
