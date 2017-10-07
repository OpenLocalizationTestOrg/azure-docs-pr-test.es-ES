---
title: aaaUse Hadoop Sqoop con doblez en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooremotely enviar Sqoop trabajos tooHDInsight mediante Curl."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Ejecución de trabajos de Sqoop con Hadoop en HDInsight con Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Obtenga información acerca de cómo agrupar toouse Curl toorun Sqoop trabajos en un Hadoop en HDInsight.

CURL es usado toodemonstrate cómo pueden interactuar con HDInsight mediante toorun de las solicitudes HTTP sin formato, monitor y recuperar los resultados de Hola de trabajos de Sqoop. Esto funciona con hello WebHCat REST API (anteriormente conocido como Templeton) proporcionado por el clúster de HDInsight.

> [!NOTE]
> Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea [información sobre el uso de HDInsight en Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
pasos de hello toocomplete en este artículo, se necesita Hola siguiente:

* Un clúster de Hadoop en HDInsight (basado en Linux o Windows)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Envío de trabajos de Sqoop mediante Curl
> [!NOTE]
> Al usar Curl o cualquier otro tipo de comunicación REST con WebHCat, debe autenticar solicitudes de hello proporcionando el nombre de usuario de Hola y la contraseña de administrador de clústeres de HDInsight Hola. También debe usar el nombre del clúster de hello como parte del identificador uniforme de recursos (URI) de hello utiliza servidor toohello de toosend hello las solicitudes.
> 
> Para los comandos de hello en esta sección, reemplace **nombre de usuario** por clúster de hello usuario tooauthenticate toohello y **contraseña** con contraseña hello para la cuenta de usuario de Hola. Reemplace **CLUSTERNAME** con nombre hello del clúster.
> 
> API de REST de Hello se protege una a través de [la autenticación básica](http://en.wikipedia.org/wiki/Basic_access_authentication). Siempre debe realizar las solicitudes mediante el uso de HTTP seguro (HTTPS) toohelp Asegúrese de que sus credenciales se envían de forma segura toohello server.
> 
> 

1. Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Debería recibir un siguiente toohello similar de respuesta:
   
        {"status":"ok","version":"v1"}
   
    parámetros de Hello utilizados en este comando son los siguientes:
   
   * **-u** -Hola nombre de usuario y una contraseña usan tooauthenticate solicitud de saludo.
   * **-G** : indica que esta es una solicitud GET.
     
     Hola a partir de la dirección URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será el mismo Hola para todas las solicitudes. ruta de acceso de Hello, **/Status**, indica esa solicitud hello es tooreturn un estado de WebHCat (también conocido como Templeton) para servidor de Hola. 
2. Usar hello después de un trabajo de sqoop toosubmit:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    parámetros de Hello utilizados en este comando son los siguientes:

    * **-d** : desde `-G` no se utiliza, solicitud de hello tiene como valor predeterminado el método POST de toohello. `-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.

        * **User.nombre** -usuario Hola que se ejecuta el comando Hola.

        * **comando** -Hola Sqoop comando tooexecute.

        * **statusdir** -directorio Hola Hola estado para este trabajo se escribirán en.

    Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de Hola.

        {"id":"job_1415651640909_0026"}

1. estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando. Reemplace **JOBID** con valor Hola devuelta en el paso anterior de Hola. Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, **JOBID** sería `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Si ha terminado el trabajo de hello, estado de hello será **correcto**.
   
   > [!NOTE]
   > Esta solicitud Curl devuelve un documento de JavaScript Object Notation (JSON) con información sobre el trabajo de hello; se utiliza jq tooretrieve Hola solo el valor de estado.
   > 
   > 
2. Una vez que el estado de Hola de trabajo de hello ha cambiado demasiado**correcto**, se pueden recuperar resultados de Hola de trabajo de Hola desde el almacenamiento de blobs de Azure. Hola `statusdir` parámetro pasado con hello consulta contiene ubicación de Hola Hola del archivo de salida; en este caso, **wasb: / / / ejemplo/curl**. Esta dirección almacena los resultados de Hola de trabajo de Hola Hola **ejemplo/curl** directorio en el contenedor de almacenamiento de hello predeterminado utilizado por el clúster de HDInsight.
   
    Puede enumerar y descargar estos archivos mediante el uso de hello [CLI de Azure](../cli-install-nodejs.md). Por ejemplo, archivos toolist en **ejemplo/curl**, usar hello siguiente comando:
   
        azure storage blob list <container-name> example/curl
   
    toodownload un archivo, utilice la siguiente de hello:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > O bien debe especificar el nombre de cuenta de almacenamiento de Hola que contiene datos de blob de hello mediante el uso de hello `-a` y `-k` parámetros o conjunto hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_acceso\_clave** variables de entorno. Vea <a href="hdinsight-upload-data.md" target="_blank" para obtener más información.
   > 
   > 

## <a name="limitations"></a>Limitaciones
* La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.
* Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop llevará a cabo varias inserciones en lugar de las operaciones de inserción de Hola de procesamiento por lotes.

## <a name="summary"></a>Resumen
Como se muestra en este documento, puede usar un toorun de solicitud HTTP sin formato, al monitor y ver los resultados de los trabajos de Sqoop hello en el clúster de HDInsight.

Para obtener más información sobre la interfaz REST de hello usan en este artículo, consulte hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Guía de la API de REST de Sqoop</a>.

## <a name="next-steps"></a>Pasos siguientes
Si desea obtener información general sobre Hive con HDInsight:

* [Uso de Sqoop con Hadoop en HDInsight (Windows)](hdinsight-use-sqoop.md)

Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


