---
title: "clúster aaaUse Livio Spark toosubmit trabajos tooSpark en HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse API de REST de Apache Spark toosubmit Spark remotamente trabajos tooan clúster de HDInsight de Azure."
keywords: API de REST de Apache Spark, Livy Spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Usar la API de REST de Apache Spark toosubmit trabajos remotos tooan clúster de HDInsight Spark

Obtenga información acerca de cómo trabajos del clúster de Azure HDInsight Spark tooan toouse Livio, Hola Apache Spark REST API, que es usado toosubmit remoto. Para obtener documentación detallada, vea [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

Puede usar los shells de Spark interactivos Livio toorun o enviar toobe de trabajos por lotes ejecutar en Spark. En este artículo se habla sobre el uso de trabajos por lotes de Livio toosubmit. fragmentos de código de Hello en este artículo usan cURL toomake punto de conexión Livio Spark toohello de llamadas de API de REST.

**Requisitos previos:**

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). En este artículo usa toodemonstrate cURL cómo toomake API de REST se llama en un clúster de HDInsight Spark.

## <a name="submit-a-livy-spark-batch-job"></a>Envío de un trabajo por lotes de Livy Spark
Antes de enviar un trabajo por lotes, debe cargar jar de aplicación hello en el almacenamiento de clúster de hello asociado con el clúster de Hola. Puede usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), una utilidad de línea de comandos, toodo para. Hay varios otros clientes que se puede usar datos de tooupload. Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Ejemplos:**

* Si es el archivo jar de hello en el almacenamiento de clúster de hello (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Si desea toopass nombre de archivo jar de Hola y Hola classname como parte de un archivo de entrada (en este ejemplo, input.txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Obtener información acerca de los lotes Livio Spark con clúster de Hola
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Ejemplos:**

* Si desea que todos los lotes de Spark Livio Hola ejecutando en el clúster de Hola tooretrieve:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Si desea que tooretrieve un lote específico con un determinado identificador de lote
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Eliminación de un trabajo por lotes de Livy Spark
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Ejemplo**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark y alta disponibilidad
Livio proporciona alta disponibilidad para los trabajos de Spark ejecutándose en el clúster de Hola. Estos son algunos ejemplos.

* Si Hola servicio Livio deja de funcionar después de que ha enviado un trabajo de forma remota tooa Spark en clúster, hello trabajo continúa toorun en segundo plano de Hola. Una vez Livio realizar copias de seguridad, restaura el estado de hello del trabajo de Hola y los informes de nuevo.
* Jupyter blocs de notas para HDInsight cuentan con la tecnología Livio en hello back-end. Si un bloc de notas está ejecutando un trabajo de Spark y obtiene reiniciar servicio Livio hello, Bloc de notas de hello continúa celdas de código de hello toorun. 

## <a name="show-me-an-example"></a>Mostrar un ejemplo
En esta sección, se mire el proceso por lotes toosubmit de ejemplos toouse Livio Spark, supervisar el progreso de Hola de trabajo de hello y, a continuación, elimínelo. aplicación que utilizamos en este ejemplo Hello es hello uno desarrollado en el artículo de hello [crear una aplicación independiente que se Scala y toorun en clúster de HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md). pasos de Hello aquí supone que:

* Ya ha copiado Hola aplicación jar toohello almacenamiento cuenta asociada con el clúster de Hola.
* Tener CuRL instalado en equipo Hola donde se intenta seguir estos pasos.

Lleve a cabo Hola pasos:

1. Permítanos primero compruebe que está ejecutando Livio Spark en clúster de Hola. Podemos hacerlo mediante la obtención de una lista de lotes en ejecución. Si está ejecutando un trabajo mediante Livio para hello primera vez, la salida de hello debe devolver cero.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Debería obtener un toohello similar de salida siguiente fragmento de código:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Tenga en cuenta cómo indica la última línea de salida de hello de hello **total: 0**, lo que no sugiere lotes en ejecución.

2. Ahora vamos a enviar un trabajo por lotes. Hola siguiente fragmento de código usa un nombre de archivo de entrada (input.txt) toopass Hola jar y un nombre de clase de hello como parámetros. Si se ejecutan estos pasos desde un equipo Windows, utilizando un archivo de entrada es Hola enfoque recomendado.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Hola parámetros en el archivo hello **input.txt** se definen como sigue:
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Debería ver un toohello similar de salida siguiente fragmento de código:
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Tenga en cuenta cómo indica la última línea de salida de hello de hello **estado: a partir de**. También indica **id:0**. En este caso, **0** es el identificador de lote Hola.

3. Ahora puede recuperar el estado de Hola de este lote específico mediante identificador de lote Hola.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Debería ver un toohello similar de salida siguiente fragmento de código:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hola de salida muestra **estado: correcto**, lo que sugiere que el trabajo de Hola se completó correctamente.

4. Si lo desea, ahora puede eliminar por lotes de Hola.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Debería ver un toohello similar de salida siguiente fragmento de código:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hola última línea de salida de hello muestra que ese lote Hola se eliminó correctamente. Eliminar un trabajo, mientras se está ejecutando, también elimina el trabajo de Hola. Si elimina un trabajo que se ha completado correctamente o en caso contrario, elimina la información sobre el trabajo de hello completamente.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Uso de Livy Spark en clústeres de HDInsight 3.5

Clúster de HDInsight 3.5, de forma predeterminada, deshabilita el uso de archivos de datos de ejemplo de tooaccess de rutas de acceso de archivo local o archivos JAR. Le recomendamos que toouse hello `wasb://` ruta de acceso en su lugar archivos JAR tooaccess archivos o datos de ejemplo de clúster de Hola. Si desea toouse la ruta de acceso local, debe actualizar la configuración de Ambari de hello en consecuencia. toodo para:

1. Vaya toohello Ambari portal para clúster Hola. Hola interfaz de usuario de Ambari Web está disponible en el clúster de HDInsight en https://**CLUSTERNAME**. azurehdidnsight.net, donde CLUSTERNAME es nombre hello del clúster.

2. En la barra de navegación izquierda de hello, haga clic en **Livio**y, a continuación, haga clic en **configuraciones**.

3. En **Livio predeterminado** Agregar nombre de la propiedad de hello `livy.file.local-dir-whitelist` y establezca su valor demasiado**"/"** si desea que el sistema de toofile de tooallow acceso completo. Si desea que el directorio específico de tooallow acceso tooa solo, especifica el directorio de toothat de ruta de acceso de hello como valor de Hola.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Envío de trabajos de Livy para un clúster en una red virtual de Azure

Si se conecta tooan clúster de HDInsight Spark desde dentro de una red Virtual de Azure, puede conectar directamente tooLivy en clúster de Hola. En tal caso, Hola dirección URL de extremo Livio es `http://<IP address of hello headnode>:8998/batches`. En este caso, **8998** es el puerto de Hola donde Livio se ejecuta en el nodo principal del clúster de Hola. Para más información sobre el acceso a los servicios en puertos no públicos, vea [Puertos utilizados por los servicios Hadoop en HDInsight](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Solución de problemas

Estas son algunas causas que pueden surgir al usar Livio para clústeres de tooSpark de envío de trabajo remoto.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>No se admite el uso de un jar externo de almacenamiento adicional de Hola

**Problema:** si su trabajo Livio Spark hace referencia a un archivo jar externo de cuenta de almacenamiento adicional de hello asociada con el clúster de hello, se produce un error en el trabajo de Hola.

**Solución:** Asegúrese de que ese jar Hola desea toouse está disponible en almacenamiento de hello predeterminado asociado con el clúster de HDInsight Hola.





## <a name="next-step"></a>Paso siguiente

* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

