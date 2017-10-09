---
title: aaaUse MapReduce y Curl con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooremotely ejecutar trabajos de MapReduce con Hadoop en HDInsight con Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>Ejecución de trabajos de MapReduce con Hadoop en HDInsight con REST

Obtenga información acerca de cómo trabajos toouse Hola API de REST de WebHCat toorun MapReduce en un Hadoop en clúster de HDInsight. CURL es usado toodemonstrate cómo pueden interactuar con HDInsight mediante trabajos de MapReduce de toorun de las solicitudes HTTP sin formato.

> [!NOTE]
> Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea hello [lo que necesita tooknow sobre basado en Linux, Hadoop en HDInsight](hdinsight-hadoop-linux-information.md) documento.


## <a id="prereq"></a>Requisitos previos

* Un clúster de Hadoop en HDInsight
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Ejecución de trabajos de MapReduce mediante Curl

> [!NOTE]
> Cuando usas Curl o cualquier otro tipo de comunicación REST con WebHCat, debe autenticar solicitudes de hello proporcionando la contraseña y nombre de usuario de administrador de clúster de HDInsight de Hola. Debe usar el nombre del clúster de hello como parte del URI que es usado toosend Hola solicitudes toohello servidor hello.
>
> Para los comandos de hello en esta sección, reemplace **nombre de usuario** con clúster de hello usuario tooauthenticate toohello, y **contraseña** con contraseña hello para la cuenta de usuario de Hola. Reemplace **CLUSTERNAME** con nombre hello del clúster.
>
> Hello API de REST se protege utilizando [autenticación de acceso básico](http://en.wikipedia.org/wiki/Basic_access_authentication). Siempre debe realizar las solicitudes mediante tooensure HTTPS que sus credenciales se envían de forma segura toohello server.


1. Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Debería recibir un toohello similar de respuesta después de JSON:

        {"status":"ok","version":"v1"}

    parámetros de Hello utilizados en este comando son los siguientes:

   * **-u**: indica Hola nombre de usuario y una contraseña usan solicitud de hello tooauthenticate
   * **-G**: indica que esta operación es una solicitud GET.

     Hola a partir de hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Hola iguales para todas las solicitudes.

2. toosubmit un trabajo MapReduce, utilice Hola siguiente comando:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    final de Hola de hello URI (/ mapreduce/jar) indica WebHCat que esta solicitud inicia un trabajo de MapReduce desde una clase en un archivo jar. parámetros de Hello utilizados en este comando son los siguientes:

   * **-d**: `-G` no se utiliza, por lo que la solicitud de hello tiene como valor predeterminado el método POST de toohello. `-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.
    * **User.nombre**: usuario de Hola que está ejecutando el comando hello
    * **JAR**: ubicación de hello del archivo jar de Hola que contiene la clase toobe se ejecutó
    * **clase**: Hola clase que contiene la lógica de MapReduce Hola
    * **arg**: Hola argumentos toobe pasa toohello trabajo de MapReduce. En este caso, Hola de entrada de directorio de hello y archivo de texto que se usa para la salida de hello

     Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de hello:

       {"id":"job_1415651640909_0026"}

3. estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Reemplace hello **JOBID** con valor Hola devuelta en el paso anterior de Hola. Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, Hola JOBID sería `job_1415651640909_0026`.

    Si el trabajo de hello está completado, el estado de hello devuelto es `SUCCEEDED`.

   > [!NOTE]
   > Esta solicitud Curl devuelve un documento JSON con información sobre el trabajo de Hola. Se utiliza Jq tooretrieve Hola solo el valor de estado.

4. Cuando el estado de Hola de trabajo de hello ha cambiado demasiado`SUCCEEDED`, se pueden recuperar resultados de Hola de trabajo de Hola desde el almacenamiento de blobs de Azure. Hola `statusdir` parámetro que se pasa con la consulta de hello contiene la ubicación de Hola Hola del archivo de salida. En este ejemplo, la ubicación de hello es `/example/curl`. Esta dirección almacena los resultados de Hola de trabajo de hello en almacenamiento de hello clústeres predeterminado en `/example/curl`.

Puede enumerar y descargar estos archivos mediante el uso de hello [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Para obtener más información sobre cómo trabajar con blobs de hello CLI de Azure, vea hello [hello mediante Azure CLI 2.0 con el almacenamiento de Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) documento.

## <a id="nextsteps"></a>Pasos siguientes

Para obtener información general sobre los trabajos de MapReduce en HDInsight:

* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)

Para obtener más información acerca de la interfaz REST de Hola que se usa en este artículo, consulte hello [WebHCat referencia](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
