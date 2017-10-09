---
title: aaaUse Hadoop Pig con REST en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo agrupar toouse REST toorun Pig latino los trabajos en un Hadoop en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Ejecución de trabajos de Pig con Hadoop en HDInsight con REST

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Obtenga información acerca de cómo toorun Pig latino trabajos mediante la realización de clúster de HDInsight de Azure de tooan de las solicitudes REST. CURL es usado toodemonstrate cómo pueden interactuar con HDInsight con la API de REST de WebHCat Hola.

> [!NOTE]
> Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea [sugerencias de HDInsight basados en Linux](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Requisitos previos

* Un clúster de HDInsight de Azure (Hadoop en HDInsight) (basado en Windows o en Linux)

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Ejecución de trabajos de Pig con Curl

> [!NOTE]
> API de REST de Hello se protege una a través de [autenticación de acceso básico](http://en.wikipedia.org/wiki/Basic_access_authentication). Siempre se realizan las solicitudes mediante el uso de tooensure HTTP seguro (HTTPS) que sus credenciales se envían de forma segura toohello server.
>
> Cuando utilice comandos de hello en esta sección, reemplace `USERNAME` por clúster de hello usuario tooauthenticate toohello y `PASSWORD` con la contraseña de hello para la cuenta de usuario de Hola. Reemplace `CLUSTERNAME` con nombre hello del clúster.
>


1. Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Debería recibir Hola después de la respuesta JSON:

        {"status":"ok","version":"v1"}

    parámetros de Hello utilizados en este comando son los siguientes:

    * **-u**: Hola nombre de usuario y la contraseña utilizan la solicitud de hello tooauthenticate
    * **-G**: indica que esta es una solicitud GET.

     Hola a partir de la dirección URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Hola iguales para todas las solicitudes. ruta de acceso de Hello, **/Status**, indica esa solicitud hello es el estado de hello tooreturn WebHCat (también conocido como Templeton) para servidor de Hola.

2. Usar hello después de un clúster de toohello de trabajo de Pig latino del código toosubmit:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    parámetros de Hello utilizados en este comando son los siguientes:

    * **-d**: porque `-G` no se utiliza, solicitud de hello tiene como valor predeterminado el método POST de toohello. `-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.

    * **User.nombre**: usuario de Hola que está ejecutando el comando hello
    * **ejecutar**: Hola Pig latino instrucciones tooexecute
    * **statusdir**: se escribió en el directorio de Hola que Hola estado para este trabajo

    > [!NOTE]
    > Tenga en cuenta que los espacios de hello en las instrucciones de Pig latino se sustituyen con hello `+` caracteres cuando se usa con el doblez.

    Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de hello, por ejemplo:

        {"id":"job_1415651640909_0026"}

3. estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Reemplace `JOBID` con el valor de hello devuelta en el paso anterior de Hola. Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, `JOBID` es `job_1415651640909_0026`.

    Si ha terminado el trabajo de hello, estado de hello es **correcto**.

    > [!NOTE]
    > Esta solicitud Curl devuelve un JavaScript Object Notation (JSON) de documentos con información sobre el trabajo de Hola y jq es tooretrieve usado Hola solo el valor de estado.

## <a id="results"></a>Visualización de resultados

Cuando el estado de Hola de trabajo de hello ha cambiado demasiado**correcto**, se pueden recuperar resultados de Hola de trabajo de Hola. Hola `statusdir` parámetro pasado con hello consulta contiene ubicación de Hola Hola del archivo de salida; en este caso, `/example/pigcurl`.

HDInsight puede usar el almacenamiento de Azure o almacén de Azure Data Lake como almacén de datos predeterminado de Hola. No hay tooget de varias maneras en datos Hola dependiendo de cuál utilizar. Para obtener más información, vea la sección de almacenamiento de Hola de hello [información de HDInsight basados en Linux](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) documento.

## <a id="summary"></a>Resumen

Como se muestra en este documento, puede usar un toorun de solicitud HTTP sin formato, al monitor y ver los resultados de los trabajos de Pig hello en el clúster de HDInsight.

Para obtener más información acerca de la interfaz REST de hello usan en este artículo, consulte hello [WebHCat referencia](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Pasos siguientes

Para obtener información general sobre Pig en HDInsight:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)

Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)
