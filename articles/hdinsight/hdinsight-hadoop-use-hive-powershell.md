---
title: Uso de Hive de Hadoop con PowerShell en HDInsight (Azure) | Microsoft Docs
description: Use PowerShell para ejecutar consultas de Hive en Hadoop en HDInsight.
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
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="eceac-103">Ejecución de consultas de Hive con PowerShell</span><span class="sxs-lookup"><span data-stu-id="eceac-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="eceac-104">En este documento se ofrece un ejemplo de uso de Azure PowerShell en el modo Grupo de recursos de Azure para ejecutar consultas de Hive en un clúster Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eceac-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="eceac-105">Este documento no ofrece una descripción detallada de las instrucciones de HiveQL que se usan en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="eceac-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="eceac-106">Para obtener información sobre el lenguaje HiveQL que se usa en este ejemplo, vea [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="eceac-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="eceac-107">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="eceac-107">**Prerequisites**</span></span>

* <span data-ttu-id="eceac-108">**Un clúster de Azure HDInsight**: no importa si el clúster está basado en Windows o en Linux.</span><span class="sxs-lookup"><span data-stu-id="eceac-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="eceac-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="eceac-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="eceac-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="eceac-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="eceac-111">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="eceac-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="eceac-112">Ejecución de consultas de Hive con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="eceac-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="eceac-113">Azure PowerShell proporciona *cmdlets* que le permiten ejecutar de manera remota las consultas de Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eceac-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="eceac-114">Internamente, los cmdlets realizan llamadas de REST a la instancia de [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eceac-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="eceac-115">Los siguientes cmdlets se utilizan al ejecutar las consultas de Hive en un clúster de HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="eceac-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="eceac-116">**Add-AzureRmAccount**: autentica a Azure PowerShell en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="eceac-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="eceac-117">**New-AzureRmHDInsightHiveJobDefinition**: crea una nueva *definición de trabajo* con las instrucciones HiveQL especificadas.</span><span class="sxs-lookup"><span data-stu-id="eceac-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="eceac-118">**Start-AzureRmHDInsightJob**: envía la definición del trabajo a HDInsight, inicia el trabajo y devuelve un objeto de *trabajo* que se puede usar para comprobar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="eceac-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="eceac-119">**Wait-AzureRmHDInsightJob**: usa el objeto de trabajo para comprobar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="eceac-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="eceac-120">Esperará hasta que el trabajo se complete o se supere el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="eceac-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="eceac-121">**Get-AzureRmHDInsightJobOutput**: se usa para recuperar la salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="eceac-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="eceac-122">**Invoke-AzureRmHDInsightHiveJob**: se usa para ejecutar instrucciones de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="eceac-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="eceac-123">Este cmdlet bloqueará la consulta completa, a continuación, devuelve los resultados.</span><span class="sxs-lookup"><span data-stu-id="eceac-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="eceac-124">**Use-AzureRmHDInsightCluster**: establece el clúster actual para usarlo para el comando **Invoke-AzureRmHDInsightHiveJob**.</span><span class="sxs-lookup"><span data-stu-id="eceac-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="eceac-125">Los pasos siguientes muestran cómo usar estos cmdlets para ejecutar un trabajo en el clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eceac-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="eceac-126">Mediante un editor, guarde el código siguiente como **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="eceac-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="eceac-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="eceac-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="eceac-128">Abra un nuevo símbolo del sistema de **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="eceac-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="eceac-129">Cambie los directorios a la ubicación del archivo **hivejob.ps1** y, a continuación, utilice el siguiente comando para ejecutar el script:</span><span class="sxs-lookup"><span data-stu-id="eceac-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="eceac-130">Cuando se ejecute el script, se le pedirá que escriba el nombre del clúster y las credenciales de la cuenta de administrador/HTTPS del clúster.</span><span class="sxs-lookup"><span data-stu-id="eceac-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="eceac-131">Puede que también se le pida que inicie la sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="eceac-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="eceac-132">Cuando el trabajo se complete, debe devolver información de manera similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="eceac-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="eceac-133">Como se mencionó anteriormente **Invoke-Hive** puede utilizarse para ejecutar una consulta y esperar la respuesta.</span><span class="sxs-lookup"><span data-stu-id="eceac-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="eceac-134">Use el siguiente script para ver cómo funciona Invoke-Hive:</span><span class="sxs-lookup"><span data-stu-id="eceac-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="eceac-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="eceac-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="eceac-136">La salida tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="eceac-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="eceac-137">Para consultas de HiveQL más extensas, puede usar el cmdlet **Here-Strings** de Azure PowerShell o archivos de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="eceac-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="eceac-138">El siguiente fragmento de código indica cómo usar el cmdlet **Invoke-Hive** para ejecutar un archivo de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="eceac-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="eceac-139">El archivo de script de HiveQL debe cargarse en wasb://.</span><span class="sxs-lookup"><span data-stu-id="eceac-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="eceac-140">Para más información acerca de **Here-Strings**, consulte <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a> (Uso de Here-Strings de Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="eceac-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="eceac-141">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="eceac-141">Troubleshooting</span></span>

<span data-ttu-id="eceac-142">Si no se devuelve ninguna información cuando se completa el trabajo, pudo haberse producido un error durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="eceac-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="eceac-143">Para ver información de error para este trabajo, agregue lo siguiente al final del archivo **hivejob.ps1** , guárdelo y, a continuación, ejecútelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="eceac-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="eceac-144">Este cmdlet devuelve la información escrita en STDERR en el servidor cuando ejecute el trabajo.</span><span class="sxs-lookup"><span data-stu-id="eceac-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="eceac-145">Resumen</span><span class="sxs-lookup"><span data-stu-id="eceac-145">Summary</span></span>

<span data-ttu-id="eceac-146">Como puede ver, Azure PowerShell proporciona una manera fácil de ejecutar consultas de Hive en un clúster de HDInsight, de supervisar el estado del trabajo y de recuperar la salida.</span><span class="sxs-lookup"><span data-stu-id="eceac-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eceac-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eceac-147">Next steps</span></span>

<span data-ttu-id="eceac-148">Para obtener información general acerca de Hive en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eceac-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="eceac-149">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eceac-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="eceac-150">Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eceac-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="eceac-151">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eceac-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="eceac-152">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="eceac-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
