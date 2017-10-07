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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>Generación de recomendaciones de películas mediante Apache Mahout con Hadoop en HDInsight (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Obtenga información acerca de cómo hello toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizaje de máquina con recomendaciones de película toogenerate de HDInsight de Azure. ejemplo de Hola en este documento utiliza Azure PowerShell toorun Mahout trabajos.

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de HDInsight basado en Linux Para obtener información sobre cómo crear uno, consulte [Introducción al uso de Hadoop en HDInsight basado en Linux][getstarted].

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>Generación de recomendaciones mediante Azure PowerShell

> [!WARNING]
> trabajo de Hello en esta sección funciona mediante el uso de PowerShell de Azure. Muchas de las clases de hello proporcionadas con Mahout actualmente no trabaja con Azure PowerShell. Para obtener una lista de clases que no funcionan con Azure PowerShell, vea hello [solución de problemas](#troubleshooting) sección.
>
> Para obtener un ejemplo del uso de SSH tooconnect tooHDInsight y ejemplos de ejecución Mahout directamente en el clúster de hello, consulte [generar recomendaciones de película mediante Mahout y HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

Una de las funciones hello proporcionada por Mahout es un motor de recomendación. Este motor acepta datos en formato de Hola de `userID`, `itemId`, y `prefValue` (Hola preferencias de los usuarios para el elemento de hello). Mahout usa Hola datos toodetermine los usuarios con las preferencias de elemento de tipo, que pueden ser usado toomake recomendaciones.

Hello en el ejemplo siguiente se es un tutorial simplificado de cómo funciona el proceso de recomendación de hello:

* **aparición coadministradores**: Joe, Alice y Bob querido todos los *estrella guerras*, *Hola Empire plenos volver*, y *devolución de hello Jedi*. Mahout determina que los usuarios que como cualquiera de estas películas también como Hola otros dos.

* **aparición coadministradores**: Roberto y Alicia también gustó *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*. Mahout determina que los usuarios que gustó películas de tres anterior hello también como estas películas.

* **Recomendación de similitud**: Joe porque gustó Hola tres primeros de películas, Mahout examina películas que otros usuarios que tengan preferencias similares gustó, pero no observarán Joe (gustó/clasificación). En este caso, se recomienda Mahout *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*.

### <a name="understanding-hello-data"></a>Descripción de los datos de Hola

[GroupLens Research][movielens] proporciona calificaciones de películas en un formato compatible con Mahout. Estos datos están disponibles en el almacenamiento predeterminado de hello para el clúster en `/HdiSamples//HdiSamples/MahoutMovieData`.

Hay dos archivos, `moviedb.txt` (información sobre películas de hello) y `user-ratings.txt`. Hola `user-ratings.txt` archivo se utiliza durante el análisis. Hola `moviedb.txt` archivo es texto descriptivo tooprovide usado al mostrar los resultados de Hola de análisis de Hola.

datos de usuario ratings.txt Hello tienen una estructura de `userID`, `movieID`, `userRating`, y `timestamp`, que nos dice cómo alta cada usuario calificado una película. Este es un ejemplo de Hola datos:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Ejecutar trabajo de Hola

Usar hello después toorun de secuencia de comandos de Windows PowerShell un trabajo que utiliza el motor de recomendaciones de hello Mahout con datos de la película de hello:

> [!NOTE]
> Este archivo le pide información de clúster de HDInsight de tooyour tooconnect utilizado y los trabajos de ejecución. Puede tardar varios minutos para toocomplete de trabajos de Hola y descargar el archivo de hello output.txt.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> Trabajos de Mahout no quite los datos temporales que se crean al procesar el trabajo de Hola. Hola `--tempDir` parámetro se especifica en archivos temporales de hello ejemplo trabajo tooisolate hello en un directorio específico.

Hola Mahout job no devuelve hello tooSTDOUT de salida. En su lugar, almacena en el directorio de salida especificado hello como **parte-r-00000**. script de Hola descarga este archivo demasiado**output.txt** en el directorio actual de hello en la estación de trabajo.

Hello texto siguiente es un ejemplo de Hola contenido de este archivo:

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

Hola primera columna es hello `userID`. Hola valores contenidos en ' [' y ']' son `movieId`:`recommendationScore`.

script de Hola también descarga hello `moviedb.txt` y `user-ratings.txt` archivos, que son necesarios tooformat Hola salida toobe sea más legible.

### <a name="view-hello-output"></a>Ver la salida de hello

Aunque hello resultado generado puede Aceptar para su uso en una aplicación, no es fácil de usar. Hola `moviedb.txt` de hello servidor puede ser usado tooresolve hello `movieId` tooa nombre de película. Usar hello siguiendo las recomendaciones de toodisplay del script de PowerShell con nombres de película:

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Usar hello sigue comando toodisplay Hola recomendaciones en un formato fácil de usar: 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

Hola de salida es toohello similar siguiente texto:

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

## <a name="troubleshooting"></a>Solución de problemas

### <a name="cannot-overwrite-files"></a>No se pueden sobrescribir los archivos

Los trabajos de Mahout no limpian los archivos temporales creados durante el procesamiento. Además, trabajos de hello no sobrescriben el archivo de salida existente.

tooavoid errores al ejecutar los trabajos de Mahout, eliminar archivos temporales y salida entre ejecuciones. archivos de hello tooremove creados por hello scripts anteriores en este documento, use Hola siguiente script de PowerShell:

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

### <a name="nopowershell"></a>Clases que no funcionan con Azure PowerShell

Trabajos de Mahout que usan Hola siguientes clases devuelven varios mensajes de error cuando se usa en Windows PowerShell:

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

trabajos de toorun que utilizan estas clases, conectan el clúster de HDInsight de toohello mediante SSH y ejecutan trabajos de Hola desde la línea de comandos de Hola. Para obtener un ejemplo del uso de SSH toorun Mahout trabajos, consulte [generar recomendaciones de película mediante Mahout y HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toouse Mahout, descubra otras formas de trabajar con datos en HDInsight:

* [Hive con HDInsight](hdinsight-use-hive.md)
* [Pig con HDInsight](hdinsight-use-pig.md)
* [MapReduce con HDInsight](hdinsight-use-mapreduce.md)

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
