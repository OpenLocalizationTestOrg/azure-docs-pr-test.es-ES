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
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>Ejecución de trabajos de MapReduce con Hadoop en HDInsight con PowerShell

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Este documento proporciona un ejemplo del uso de PowerShell de Azure toorun un trabajo MapReduce en un Hadoop en clúster de HDInsight.

## <a id="prereq"></a>Requisitos previos

* **Un clúster de HDInsight (Hadoop en HDInsight)**.

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Una estación de trabajo con Azure PowerShell**.

## <a id="powershell"></a>Ejecución de un trabajo de MapReduce mediante Azure PowerShell

Azure PowerShell ofrece *cmdlets* que le permiten tooremotely ejecutar trabajos de MapReduce en HDInsight. Internamente, esto se logra mediante llamadas a REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (anteriormente denominados Templeton) se ejecuta en Hola clúster de HDInsight.

Hello siguientes cmdlets se utilizan al ejecutar los trabajos de MapReduce en un clúster de HDInsight remoto.

* **Inicio de sesión AzureRmAccount**: autentica Azure PowerShell tooyour suscripción de Azure.

* **Nueva AzureRmHDInsightMapReduceJobDefinition**: crea un nuevo *definición de trabajo* mediante el uso de hello especifica información de MapReduce.

* **Start-AzureRmHDInsightJob**: envía tooHDInsight de definición de trabajo de hello, inicia el trabajo de Hola y devuelve un *trabajo* objetos que pueden ser utilizados toocheck Hola estado del trabajo de Hola.

* **Espera AzureRmHDInsightJob**: utiliza el estado del objeto toocheck Hola de hello trabajo del trabajo de Hola. Espera hasta que complete el trabajo de Hola o se supera el tiempo de espera de Hola.

* **Get-AzureRmHDInsightJobOutput**: utiliza la salida de hello tooretrieve de trabajo de Hola.

Hello pasos siguientes demuestran cómo toouse estos toorun cmdlets un trabajo en el clúster de HDInsight.

1. Con el editor, guardar Hola siguiente código como **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Abra un nuevo símbolo del sistema de **Azure PowerShell** . Cambiar ubicación de toohello de directorios de hello **mapreducejob.ps1** de archivos, a continuación, usar hello sigue la secuencia de comandos de Hola toorun:

        .\mapreducejob.ps1

    Al ejecutar el script de Hola, le pediremos nombre Hola Hola del clúster de HDInsight y nombre de la cuenta de hello HTTPS/Admin y la contraseña para el clúster de Hola. También es posible que tooauthenticate solicitadas tooyour suscripción de Azure.

3. Cuando se completa el trabajo de hello, recibirá toohello similar de salida siguiente texto:

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Este resultado indica que el trabajo de Hola se completó correctamente.

    > [!NOTE]
    > Si hello **ExitCode** es un valor distinto de 0, vea [solución de problemas](#troubleshooting).

    En este ejemplo también almacena Hola descargan archivos tooan **output.txt** archivo directorio Hola que ejecutar script de Hola de.

### <a name="view-output"></a>Visualización de la salida

Abra hello **output.txt** archivo en un hello toosee de editor de texto es decir y cuenta producido por trabajo Hola.

> [!NOTE]
> archivos de salida de Hello de un trabajo de MapReduce son inmutables. Por lo que si se vuelve a ejecutar este ejemplo, necesita toochange Hola nombre hello del archivo de salida.

## <a id="troubleshooting"></a>Solución de problemas

Si no se devuelve información cuando se completa el trabajo de hello, puede deberse a un error durante el procesamiento. información de error de tooview para este trabajo, agregar Hola siguiente comando toohello final de hello **mapreducejob.ps1** archivo, guárdelo y, a continuación, vuelva a ejecutarlo.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Este cmdlet devuelve información de Hola que escribió tooSTDERR en servidor hello cuando ejecutó el trabajo de Hola y puede ayudar a determinar por qué se producen errores en trabajo Hola.

## <a id="summary"></a>Resumen

Como puede ver, Azure PowerShell ofrece una manera sencilla de toorun trabajos MapReduce en un clúster de HDInsight, supervisar el estado de trabajo de Hola y salida de hello de recuperar.

## <a id="nextsteps"></a>Pasos siguientes

Para obtener información general sobre los trabajos de MapReduce en HDInsight:

* [Uso de MapReduce en Hadoop de HDInsight](hdinsight-use-mapreduce.md)

Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
