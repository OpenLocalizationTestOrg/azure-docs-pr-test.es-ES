---
title: recomendaciones de aaaGenerate con Mahout HDInsight desde PowerShell - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola máquina Apache Mahout aprendizaje recomendaciones de película toogenerate de biblioteca con HDInsight (Hadoop) desde un script de PowerShell que se ejecuta en el cliente."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="e739e-103">Generación de recomendaciones de películas mediante Apache Mahout con Hadoop en HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e739e-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="e739e-104">Obtenga información acerca de cómo hello toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizaje de máquina con recomendaciones de película toogenerate de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="e739e-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="e739e-105">ejemplo de Hola en este documento utiliza Azure PowerShell toorun Mahout trabajos.</span><span class="sxs-lookup"><span data-stu-id="e739e-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e739e-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e739e-106">Prerequisites</span></span>

* <span data-ttu-id="e739e-107">Un clúster de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="e739e-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e739e-108">Para obtener información sobre cómo crear uno, consulte [Introducción al uso de Hadoop en HDInsight basado en Linux][getstarted].</span><span class="sxs-lookup"><span data-stu-id="e739e-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e739e-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="e739e-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e739e-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e739e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="e739e-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e739e-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="e739e-112"><a name="recommendations"></a>Generación de recomendaciones mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e739e-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="e739e-113">trabajo de Hello en esta sección funciona mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="e739e-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="e739e-114">Muchas de las clases de hello proporcionadas con Mahout actualmente no trabaja con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e739e-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="e739e-115">Para obtener una lista de clases que no funcionan con Azure PowerShell, vea hello [solución de problemas](#troubleshooting) sección.</span><span class="sxs-lookup"><span data-stu-id="e739e-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="e739e-116">Para obtener un ejemplo del uso de SSH tooconnect tooHDInsight y ejemplos de ejecución Mahout directamente en el clúster de hello, consulte [generar recomendaciones de película mediante Mahout y HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="e739e-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="e739e-117">Una de las funciones hello proporcionada por Mahout es un motor de recomendación.</span><span class="sxs-lookup"><span data-stu-id="e739e-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="e739e-118">Este motor acepta datos en formato de Hola de `userID`, `itemId`, y `prefValue` (Hola preferencias de los usuarios para el elemento de hello).</span><span class="sxs-lookup"><span data-stu-id="e739e-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="e739e-119">Mahout usa Hola datos toodetermine los usuarios con las preferencias de elemento de tipo, que pueden ser usado toomake recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="e739e-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="e739e-120">Hello en el ejemplo siguiente se es un tutorial simplificado de cómo funciona el proceso de recomendación de hello:</span><span class="sxs-lookup"><span data-stu-id="e739e-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="e739e-121">**aparición coadministradores**: Joe, Alice y Bob querido todos los *estrella guerras*, *Hola Empire plenos volver*, y *devolución de hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="e739e-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="e739e-122">Mahout determina que los usuarios que como cualquiera de estas películas también como Hola otros dos.</span><span class="sxs-lookup"><span data-stu-id="e739e-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="e739e-123">**aparición coadministradores**: Roberto y Alicia también gustó *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="e739e-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="e739e-124">Mahout determina que los usuarios que gustó películas de tres anterior hello también como estas películas.</span><span class="sxs-lookup"><span data-stu-id="e739e-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="e739e-125">**Recomendación de similitud**: Joe porque gustó Hola tres primeros de películas, Mahout examina películas que otros usuarios que tengan preferencias similares gustó, pero no observarán Joe (gustó/clasificación).</span><span class="sxs-lookup"><span data-stu-id="e739e-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="e739e-126">En este caso, se recomienda Mahout *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="e739e-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="e739e-127">Descripción de los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="e739e-127">Understanding hello data</span></span>

<span data-ttu-id="e739e-128">[GroupLens Research][movielens] proporciona calificaciones de películas en un formato compatible con Mahout.</span><span class="sxs-lookup"><span data-stu-id="e739e-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="e739e-129">Estos datos están disponibles en el almacenamiento predeterminado de hello para el clúster en `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="e739e-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="e739e-130">Hay dos archivos, `moviedb.txt` (información sobre películas de hello) y `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="e739e-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="e739e-131">Hola `user-ratings.txt` archivo se utiliza durante el análisis.</span><span class="sxs-lookup"><span data-stu-id="e739e-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="e739e-132">Hola `moviedb.txt` archivo es texto descriptivo tooprovide usado al mostrar los resultados de Hola de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="e739e-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="e739e-133">datos de usuario ratings.txt Hello tienen una estructura de `userID`, `movieID`, `userRating`, y `timestamp`, que nos dice cómo alta cada usuario calificado una película.</span><span class="sxs-lookup"><span data-stu-id="e739e-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="e739e-134">Este es un ejemplo de Hola datos:</span><span class="sxs-lookup"><span data-stu-id="e739e-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="e739e-135">Ejecutar trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="e739e-135">Run hello job</span></span>

<span data-ttu-id="e739e-136">Usar hello después toorun de secuencia de comandos de Windows PowerShell un trabajo que utiliza el motor de recomendaciones de hello Mahout con datos de la película de hello:</span><span class="sxs-lookup"><span data-stu-id="e739e-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="e739e-137">Este archivo le pide información de clúster de HDInsight de tooyour tooconnect utilizado y los trabajos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e739e-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="e739e-138">Puede tardar varios minutos para toocomplete de trabajos de Hola y descargar el archivo de hello output.txt.</span><span class="sxs-lookup"><span data-stu-id="e739e-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="e739e-139">Trabajos de Mahout no quite los datos temporales que se crean al procesar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e739e-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="e739e-140">Hola `--tempDir` parámetro se especifica en archivos temporales de hello ejemplo trabajo tooisolate hello en un directorio específico.</span><span class="sxs-lookup"><span data-stu-id="e739e-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="e739e-141">Hola Mahout job no devuelve hello tooSTDOUT de salida.</span><span class="sxs-lookup"><span data-stu-id="e739e-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="e739e-142">En su lugar, almacena en el directorio de salida especificado hello como **parte-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="e739e-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="e739e-143">script de Hola descarga este archivo demasiado**output.txt** en el directorio actual de hello en la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e739e-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="e739e-144">Hello texto siguiente es un ejemplo de Hola contenido de este archivo:</span><span class="sxs-lookup"><span data-stu-id="e739e-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="e739e-145">Hola primera columna es hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="e739e-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="e739e-146">Hola valores contenidos en ' [' y ']' son `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="e739e-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="e739e-147">script de Hola también descarga hello `moviedb.txt` y `user-ratings.txt` archivos, que son necesarios tooformat Hola salida toobe sea más legible.</span><span class="sxs-lookup"><span data-stu-id="e739e-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="e739e-148">Ver la salida de hello</span><span class="sxs-lookup"><span data-stu-id="e739e-148">View hello output</span></span>

<span data-ttu-id="e739e-149">Aunque hello resultado generado puede Aceptar para su uso en una aplicación, no es fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="e739e-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="e739e-150">Hola `moviedb.txt` de hello servidor puede ser usado tooresolve hello `movieId` tooa nombre de película.</span><span class="sxs-lookup"><span data-stu-id="e739e-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="e739e-151">Usar hello siguiendo las recomendaciones de toodisplay del script de PowerShell con nombres de película:</span><span class="sxs-lookup"><span data-stu-id="e739e-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="e739e-152">Usar hello sigue comando toodisplay Hola recomendaciones en un formato fácil de usar:</span><span class="sxs-lookup"><span data-stu-id="e739e-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="e739e-153">Hola de salida es toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e739e-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="e739e-154"><a name="troubleshooting"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e739e-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="e739e-155">No se pueden sobrescribir los archivos</span><span class="sxs-lookup"><span data-stu-id="e739e-155">Cannot overwrite files</span></span>

<span data-ttu-id="e739e-156">Los trabajos de Mahout no limpian los archivos temporales creados durante el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="e739e-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="e739e-157">Además, trabajos de hello no sobrescriben el archivo de salida existente.</span><span class="sxs-lookup"><span data-stu-id="e739e-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="e739e-158">tooavoid errores al ejecutar los trabajos de Mahout, eliminar archivos temporales y salida entre ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="e739e-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="e739e-159">archivos de hello tooremove creados por hello scripts anteriores en este documento, use Hola siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e739e-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="e739e-160"><a name="nopowershell"></a>Clases que no funcionan con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e739e-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="e739e-161">Trabajos de Mahout que usan Hola siguientes clases devuelven varios mensajes de error cuando se usa en Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e739e-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="e739e-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="e739e-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="e739e-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="e739e-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="e739e-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="e739e-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="e739e-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="e739e-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="e739e-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="e739e-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="e739e-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="e739e-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="e739e-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="e739e-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="e739e-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="e739e-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="e739e-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="e739e-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="e739e-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="e739e-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="e739e-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="e739e-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="e739e-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="e739e-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="e739e-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="e739e-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="e739e-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="e739e-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="e739e-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="e739e-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="e739e-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="e739e-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="e739e-178">trabajos de toorun que utilizan estas clases, conectan el clúster de HDInsight de toohello mediante SSH y ejecutan trabajos de Hola desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e739e-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="e739e-179">Para obtener un ejemplo del uso de SSH toorun Mahout trabajos, consulte [generar recomendaciones de película mediante Mahout y HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="e739e-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e739e-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e739e-180">Next steps</span></span>

<span data-ttu-id="e739e-181">Ahora que ha aprendido cómo toouse Mahout, descubra otras formas de trabajar con datos en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e739e-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="e739e-182">Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e739e-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e739e-183">Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e739e-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e739e-184">MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e739e-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
