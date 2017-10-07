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
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Utilice trabajos de Pig de Azure PowerShell toorun con HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Este documento proporciona un ejemplo del uso de PowerShell de Azure toosubmit Pig trabajos tooa Hadoop en clúster de HDInsight. Pig permite toowrite MapReduce trabajos mediante el lenguaje (Pig latino) que modela las transformaciones de datos, en lugar de asignar y reducir las funciones.

> [!NOTE]
> Este documento no proporciona una descripción detallada de lo que las instrucciones de Pig latino Hola usadas en ejemplos de hello. Para obtener información acerca de hello latino Pig utilizado en este ejemplo, vea [uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md).

## <a id="prereq"></a>Requisitos previos

* **Un clúster de Azure HDInsight**.

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Una estación de trabajo con Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>Ejecución de trabajos de Pig mediante PowerShell

Azure PowerShell ofrece *cmdlets* que le permiten tooremotely ejecutar trabajos de Pig en HDInsight. Internamente, PowerShell usa llamadas REST demasiado[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) con clúster de HDInsight Hola.

Hello siguientes cmdlets se utilizan al ejecutar los trabajos de Pig en un clúster de HDInsight remoto:

* **Inicio de sesión AzureRmAccount**: autentica Azure PowerShell tooyour suscripción de Azure
* **Nueva AzureRmHDInsightPigJobDefinition**: crea un *definición de trabajo* mediante el uso de hello especifica instrucciones de Pig latino
* **Start-AzureRmHDInsightJob**: envía tooHDInsight de definición de trabajo de hello, inicia el trabajo de Hola y devuelve un *trabajo* objetos que pueden ser utilizados toocheck Hola estado del trabajo de Hola
* **Espera AzureRmHDInsightJob**: utiliza el estado del objeto toocheck Hola de hello trabajo del trabajo de Hola. Espera hasta que se haya completado el trabajo de hello, o se ha superado el tiempo de espera de Hola.
* **Get-AzureRmHDInsightJobOutput**: utiliza la salida de hello tooretrieve de trabajo de Hola

Hello pasos siguientes demuestran cómo toouse estos toorun cmdlets un trabajo en el clúster de HDInsight.

1. Con el editor, guardar Hola siguiente código como **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Abra un nuevo símbolo del sistema de Windows PowerShell. Cambiar ubicación de toohello de directorios de hello **pigjob.ps1** de archivos, a continuación, usar hello sigue la secuencia de comandos de Hola toorun:

        .\pigjob.ps1

    Son toolog solicitada en tooyour suscripción de Azure. A continuación, se le pedirán Hola HTTPs/Admin nombre y la contraseña para el clúster de HDInsight Hola.

2. Cuando se completa el trabajo de hello, debe devolver información toohello similar siguiente texto:

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Solución de problemas

Si no se devuelve información cuando se completa el trabajo de hello, puede deberse a un error durante el procesamiento. información de error de tooview para este trabajo, agregar Hola siguiente comando toohello final de hello **pigjob.ps1** archivo, guárdelo y, a continuación, vuelva a ejecutarlo.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Devuelve información de Hola que escribió tooSTDERR en servidor hello cuando ejecutó el trabajo de Hola y puede ayudar a determinar por qué se producen errores en trabajo Hola.

## <a id="summary"></a>Resumen
Como puede ver, Azure PowerShell ofrece una manera sencilla de toorun trabajos de Pig en un clúster de HDInsight, supervisar el estado de trabajo de Hola y salida de hello de recuperar.

## <a id="nextsteps"></a>Pasos siguientes
Para obtener información general sobre Pig en HDInsight, siga estos pasos:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)

Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)
