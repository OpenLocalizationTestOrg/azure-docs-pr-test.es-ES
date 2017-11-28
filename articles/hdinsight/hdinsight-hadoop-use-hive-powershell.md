---
title: aaaUse Hive de Hadoop con PowerShell en HDInsight - Azure | Documentos de Microsoft
description: Usar consultas de PowerShell toorun Hive en Hadoop en HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="77a51-103">Ejecución de consultas de Hive con PowerShell</span><span class="sxs-lookup"><span data-stu-id="77a51-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="77a51-104">Este documento proporciona un ejemplo sobre cómo usar PowerShell de Azure en consultas de Hive de toorun en modo de grupo de recursos de Azure de hello en un Hadoop en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77a51-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="77a51-105">Este documento no proporciona una descripción detallada de lo que las instrucciones de HiveQL de Hola que se utilizan en los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="77a51-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="77a51-106">Para obtener información sobre hello HiveQL que se usa en este ejemplo, vea [uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="77a51-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="77a51-107">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="77a51-107">**Prerequisites**</span></span>

* <span data-ttu-id="77a51-108">**Un clúster de HDInsight de Azure**: no importa si el clúster de hello es Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="77a51-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="77a51-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="77a51-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="77a51-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="77a51-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="77a51-111">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="77a51-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="77a51-112">Ejecución de consultas de Hive con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77a51-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="77a51-113">Azure PowerShell ofrece *cmdlets* que le permiten tooremotely ejecutar consultas de Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77a51-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="77a51-114">Internamente, los cmdlets de hello realizar llamadas REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="77a51-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="77a51-115">Hello siguientes cmdlets se utilizan cuando se ejecutan consultas de Hive en un clúster de HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="77a51-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="77a51-116">**AzureRmAccount agregar**: autentica Azure PowerShell tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="77a51-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="77a51-117">**Nueva AzureRmHDInsightHiveJobDefinition**: crea un *definición de trabajo* mediante el uso de hello especifica las instrucciones de HiveQL</span><span class="sxs-lookup"><span data-stu-id="77a51-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="77a51-118">**Start-AzureRmHDInsightJob**: envía tooHDInsight de definición de trabajo de hello, inicia el trabajo de Hola y devuelve un *trabajo* objetos que pueden ser utilizados toocheck Hola estado del trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="77a51-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="77a51-119">**Espera AzureRmHDInsightJob**: utiliza el estado del objeto toocheck Hola de hello trabajo del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="77a51-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="77a51-120">Espera hasta que complete el trabajo de Hola o se supera el tiempo de espera de Hola.</span><span class="sxs-lookup"><span data-stu-id="77a51-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="77a51-121">**Get-AzureRmHDInsightJobOutput**: utiliza la salida de hello tooretrieve de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="77a51-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="77a51-122">**AzureRmHDInsightHiveJob invocar**: utilizar instrucciones de HiveQL toorun.</span><span class="sxs-lookup"><span data-stu-id="77a51-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="77a51-123">Esta consulta de Hola de bloques de cmdlet completa, a continuación, devuelve los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="77a51-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="77a51-124">**Use AzureRmHDInsightCluster**: conjuntos de Hola toouse de clúster actual para hello **Invoke-AzureRmHDInsightHiveJob** comando</span><span class="sxs-lookup"><span data-stu-id="77a51-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="77a51-125">Hello pasos siguientes demuestran cómo toouse estos toorun cmdlets un trabajo en el clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77a51-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="77a51-126">Con el editor, guardar Hola siguiente código como **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="77a51-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="77a51-127">Abra un nuevo símbolo del sistema de **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="77a51-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="77a51-128">Cambiar ubicación de toohello de directorios de hello **hivejob.ps1** de archivos, a continuación, usar hello sigue la secuencia de comandos de Hola toorun:</span><span class="sxs-lookup"><span data-stu-id="77a51-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="77a51-129">Cuando se ejecuta el script de Hola, son tooenter solicitadas Hola clúster hello y nombre HTTPS/Admin credenciales de cuenta para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="77a51-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="77a51-130">También es posible que toolog solicitada en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="77a51-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="77a51-131">Cuando se completa el trabajo de hello, devuelve información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="77a51-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="77a51-132">Como se mencionó anteriormente, **Invoke-Hive** puede ser toorun usa una consulta y esperar respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="77a51-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="77a51-133">Usar hello después toosee script el funcionamiento de Invoke-Hive:</span><span class="sxs-lookup"><span data-stu-id="77a51-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="77a51-134">salida de Hello es similar a Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="77a51-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="77a51-135">Para consultas de HiveQL más larga, puede usar hello Azure PowerShell **Here-Strings** archivos de script de cmdlet o HiveQL.</span><span class="sxs-lookup"><span data-stu-id="77a51-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="77a51-136">Hola fragmento siguiente muestra cómo hello toouse **Invoke-Hive** cmdlet toorun un archivo de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="77a51-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="77a51-137">debe ser el archivo de script de HiveQL Hello cargado toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="77a51-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="77a51-138">Para más información acerca de **Here-Strings**, consulte <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a> (Uso de Here-Strings de Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="77a51-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="77a51-139">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="77a51-139">Troubleshooting</span></span>

<span data-ttu-id="77a51-140">Si no se devuelve información cuando se completa el trabajo de hello, puede deberse a un error durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="77a51-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="77a51-141">información de error de tooview para este trabajo, agregar Hola siguiente toohello final de hello **hivejob.ps1** archivo, guárdelo y, a continuación, vuelva a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="77a51-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="77a51-142">Este cmdlet devuelve información de Hola que se escribe tooSTDERR servidor hello cuando ejecutó el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="77a51-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="77a51-143">Resumen</span><span class="sxs-lookup"><span data-stu-id="77a51-143">Summary</span></span>

<span data-ttu-id="77a51-144">Como puede ver, Azure PowerShell ofrece una manera sencilla de toorun consultas de Hive en un clúster de HDInsight, Hola monitor Estado del trabajo y recuperar la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="77a51-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77a51-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77a51-145">Next steps</span></span>

<span data-ttu-id="77a51-146">Para obtener información general acerca de Hive en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77a51-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="77a51-147">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="77a51-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="77a51-148">Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77a51-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="77a51-149">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="77a51-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="77a51-150">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="77a51-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
