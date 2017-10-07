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
# <a name="run-hive-queries-using-powershell"></a>Ejecución de consultas de Hive con PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Este documento proporciona un ejemplo sobre cómo usar PowerShell de Azure en consultas de Hive de toorun en modo de grupo de recursos de Azure de hello en un Hadoop en clúster de HDInsight.

> [!NOTE]
> Este documento no proporciona una descripción detallada de lo que las instrucciones de HiveQL de Hola que se utilizan en los ejemplos de hello. Para obtener información sobre hello HiveQL que se usa en este ejemplo, vea [uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md).

**Requisitos previos**

* **Un clúster de HDInsight de Azure**: no importa si el clúster de hello es Windows o Linux.

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Una estación de trabajo con Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Ejecución de consultas de Hive con Azure PowerShell

Azure PowerShell ofrece *cmdlets* que le permiten tooremotely ejecutar consultas de Hive en HDInsight. Internamente, los cmdlets de hello realizar llamadas REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) en clúster de HDInsight Hola.

Hello siguientes cmdlets se utilizan cuando se ejecutan consultas de Hive en un clúster de HDInsight remoto:

* **AzureRmAccount agregar**: autentica Azure PowerShell tooyour suscripción de Azure
* **Nueva AzureRmHDInsightHiveJobDefinition**: crea un *definición de trabajo* mediante el uso de hello especifica las instrucciones de HiveQL
* **Start-AzureRmHDInsightJob**: envía tooHDInsight de definición de trabajo de hello, inicia el trabajo de Hola y devuelve un *trabajo* objetos que pueden ser utilizados toocheck Hola estado del trabajo de Hola
* **Espera AzureRmHDInsightJob**: utiliza el estado del objeto toocheck Hola de hello trabajo del trabajo de Hola. Espera hasta que complete el trabajo de Hola o se supera el tiempo de espera de Hola.
* **Get-AzureRmHDInsightJobOutput**: utiliza la salida de hello tooretrieve de trabajo de Hola
* **AzureRmHDInsightHiveJob invocar**: utilizar instrucciones de HiveQL toorun. Esta consulta de Hola de bloques de cmdlet completa, a continuación, devuelve los resultados de Hola
* **Use AzureRmHDInsightCluster**: conjuntos de Hola toouse de clúster actual para hello **Invoke-AzureRmHDInsightHiveJob** comando

Hello pasos siguientes demuestran cómo toouse estos toorun cmdlets un trabajo en el clúster de HDInsight:

1. Con el editor, guardar Hola siguiente código como **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Abra un nuevo símbolo del sistema de **Azure PowerShell** . Cambiar ubicación de toohello de directorios de hello **hivejob.ps1** de archivos, a continuación, usar hello sigue la secuencia de comandos de Hola toorun:

        .\hivejob.ps1

    Cuando se ejecuta el script de Hola, son tooenter solicitadas Hola clúster hello y nombre HTTPS/Admin credenciales de cuenta para el clúster de Hola. También es posible que toolog solicitada en tooyour suscripción de Azure.

3. Cuando se completa el trabajo de hello, devuelve información toohello similar siguiente texto:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Como se mencionó anteriormente, **Invoke-Hive** puede ser toorun usa una consulta y esperar respuesta de Hola. Usar hello después toosee script el funcionamiento de Invoke-Hive:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    salida de Hello es similar a Hola siguiente texto:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Para consultas de HiveQL más larga, puede usar hello Azure PowerShell **Here-Strings** archivos de script de cmdlet o HiveQL. Hola fragmento siguiente muestra cómo hello toouse **Invoke-Hive** cmdlet toorun un archivo de script de HiveQL. debe ser el archivo de script de HiveQL Hello cargado toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Para más información acerca de **Here-Strings**, consulte <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a> (Uso de Here-Strings de Windows PowerShell).

## <a name="troubleshooting"></a>Solución de problemas

Si no se devuelve información cuando se completa el trabajo de hello, puede deberse a un error durante el procesamiento. información de error de tooview para este trabajo, agregar Hola siguiente toohello final de hello **hivejob.ps1** archivo, guárdelo y, a continuación, vuelva a ejecutarlo.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Este cmdlet devuelve información de Hola que se escribe tooSTDERR servidor hello cuando ejecutó el trabajo de Hola.

## <a name="summary"></a>Resumen

Como puede ver, Azure PowerShell ofrece una manera sencilla de toorun consultas de Hive en un clúster de HDInsight, Hola monitor Estado del trabajo y recuperar la salida de hello.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información general acerca de Hive en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)

Para obtener información sobre otras maneras en que puede trabajar con Hadoop en HDInsight:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)
