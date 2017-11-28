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
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="af8bb-104">Usar la API de REST de Apache Spark toosubmit trabajos remotos tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="af8bb-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="af8bb-105">Obtenga información acerca de cómo trabajos del clúster de Azure HDInsight Spark tooan toouse Livio, Hola Apache Spark REST API, que es usado toosubmit remoto.</span><span class="sxs-lookup"><span data-stu-id="af8bb-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="af8bb-106">Para obtener documentación detallada, vea [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="af8bb-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="af8bb-107">Puede usar los shells de Spark interactivos Livio toorun o enviar toobe de trabajos por lotes ejecutar en Spark.</span><span class="sxs-lookup"><span data-stu-id="af8bb-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="af8bb-108">En este artículo se habla sobre el uso de trabajos por lotes de Livio toosubmit.</span><span class="sxs-lookup"><span data-stu-id="af8bb-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="af8bb-109">fragmentos de código de Hello en este artículo usan cURL toomake punto de conexión Livio Spark toohello de llamadas de API de REST.</span><span class="sxs-lookup"><span data-stu-id="af8bb-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="af8bb-110">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="af8bb-110">**Prerequisites:**</span></span>

* <span data-ttu-id="af8bb-111">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af8bb-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="af8bb-112">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="af8bb-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="af8bb-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="af8bb-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="af8bb-114">En este artículo usa toodemonstrate cURL cómo toomake API de REST se llama en un clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="af8bb-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="af8bb-115">Envío de un trabajo por lotes de Livy Spark</span><span class="sxs-lookup"><span data-stu-id="af8bb-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="af8bb-116">Antes de enviar un trabajo por lotes, debe cargar jar de aplicación hello en el almacenamiento de clúster de hello asociado con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="af8bb-117">Puede usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), una utilidad de línea de comandos, toodo para.</span><span class="sxs-lookup"><span data-stu-id="af8bb-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="af8bb-118">Hay varios otros clientes que se puede usar datos de tooupload.</span><span class="sxs-lookup"><span data-stu-id="af8bb-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="af8bb-119">Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="af8bb-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="af8bb-120">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="af8bb-120">**Examples**:</span></span>

* <span data-ttu-id="af8bb-121">Si es el archivo jar de hello en el almacenamiento de clúster de hello (WASB)</span><span class="sxs-lookup"><span data-stu-id="af8bb-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="af8bb-122">Si desea toopass nombre de archivo jar de Hola y Hola classname como parte de un archivo de entrada (en este ejemplo, input.txt)</span><span class="sxs-lookup"><span data-stu-id="af8bb-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="af8bb-123">Obtener información acerca de los lotes Livio Spark con clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="af8bb-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="af8bb-124">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="af8bb-124">**Examples**:</span></span>

* <span data-ttu-id="af8bb-125">Si desea que todos los lotes de Spark Livio Hola ejecutando en el clúster de Hola tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="af8bb-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="af8bb-126">Si desea que tooretrieve un lote específico con un determinado identificador de lote</span><span class="sxs-lookup"><span data-stu-id="af8bb-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="af8bb-127">Eliminación de un trabajo por lotes de Livy Spark</span><span class="sxs-lookup"><span data-stu-id="af8bb-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="af8bb-128">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="af8bb-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="af8bb-129">Livy Spark y alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="af8bb-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="af8bb-130">Livio proporciona alta disponibilidad para los trabajos de Spark ejecutándose en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="af8bb-131">Estos son algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="af8bb-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="af8bb-132">Si Hola servicio Livio deja de funcionar después de que ha enviado un trabajo de forma remota tooa Spark en clúster, hello trabajo continúa toorun en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="af8bb-133">Una vez Livio realizar copias de seguridad, restaura el estado de hello del trabajo de Hola y los informes de nuevo.</span><span class="sxs-lookup"><span data-stu-id="af8bb-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="af8bb-134">Jupyter blocs de notas para HDInsight cuentan con la tecnología Livio en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="af8bb-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="af8bb-135">Si un bloc de notas está ejecutando un trabajo de Spark y obtiene reiniciar servicio Livio hello, Bloc de notas de hello continúa celdas de código de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="af8bb-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="af8bb-136">Mostrar un ejemplo</span><span class="sxs-lookup"><span data-stu-id="af8bb-136">Show me an example</span></span>
<span data-ttu-id="af8bb-137">En esta sección, se mire el proceso por lotes toosubmit de ejemplos toouse Livio Spark, supervisar el progreso de Hola de trabajo de hello y, a continuación, elimínelo.</span><span class="sxs-lookup"><span data-stu-id="af8bb-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="af8bb-138">aplicación que utilizamos en este ejemplo Hello es hello uno desarrollado en el artículo de hello [crear una aplicación independiente que se Scala y toorun en clúster de HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="af8bb-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="af8bb-139">pasos de Hello aquí supone que:</span><span class="sxs-lookup"><span data-stu-id="af8bb-139">hello steps here assume that:</span></span>

* <span data-ttu-id="af8bb-140">Ya ha copiado Hola aplicación jar toohello almacenamiento cuenta asociada con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="af8bb-141">Tener CuRL instalado en equipo Hola donde se intenta seguir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="af8bb-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="af8bb-142">Lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="af8bb-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="af8bb-143">Permítanos primero compruebe que está ejecutando Livio Spark en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="af8bb-144">Podemos hacerlo mediante la obtención de una lista de lotes en ejecución.</span><span class="sxs-lookup"><span data-stu-id="af8bb-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="af8bb-145">Si está ejecutando un trabajo mediante Livio para hello primera vez, la salida de hello debe devolver cero.</span><span class="sxs-lookup"><span data-stu-id="af8bb-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="af8bb-146">Debería obtener un toohello similar de salida siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="af8bb-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="af8bb-147">Tenga en cuenta cómo indica la última línea de salida de hello de hello **total: 0**, lo que no sugiere lotes en ejecución.</span><span class="sxs-lookup"><span data-stu-id="af8bb-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="af8bb-148">Ahora vamos a enviar un trabajo por lotes.</span><span class="sxs-lookup"><span data-stu-id="af8bb-148">Let us now submit a batch job.</span></span> <span data-ttu-id="af8bb-149">Hola siguiente fragmento de código usa un nombre de archivo de entrada (input.txt) toopass Hola jar y un nombre de clase de hello como parámetros.</span><span class="sxs-lookup"><span data-stu-id="af8bb-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="af8bb-150">Si se ejecutan estos pasos desde un equipo Windows, utilizando un archivo de entrada es Hola enfoque recomendado.</span><span class="sxs-lookup"><span data-stu-id="af8bb-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="af8bb-151">Hola parámetros en el archivo hello **input.txt** se definen como sigue:</span><span class="sxs-lookup"><span data-stu-id="af8bb-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="af8bb-152">Debería ver un toohello similar de salida siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="af8bb-152">You should see an output similar toohello  following snippet:</span></span>
   
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
   
    <span data-ttu-id="af8bb-153">Tenga en cuenta cómo indica la última línea de salida de hello de hello **estado: a partir de**.</span><span class="sxs-lookup"><span data-stu-id="af8bb-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="af8bb-154">También indica **id:0**.</span><span class="sxs-lookup"><span data-stu-id="af8bb-154">It also says, **id:0**.</span></span> <span data-ttu-id="af8bb-155">En este caso, **0** es el identificador de lote Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="af8bb-156">Ahora puede recuperar el estado de Hola de este lote específico mediante identificador de lote Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="af8bb-157">Debería ver un toohello similar de salida siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="af8bb-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="af8bb-158">Hola de salida muestra **estado: correcto**, lo que sugiere que el trabajo de Hola se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="af8bb-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="af8bb-159">Si lo desea, ahora puede eliminar por lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="af8bb-160">Debería ver un toohello similar de salida siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="af8bb-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="af8bb-161">Hola última línea de salida de hello muestra que ese lote Hola se eliminó correctamente.</span><span class="sxs-lookup"><span data-stu-id="af8bb-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="af8bb-162">Eliminar un trabajo, mientras se está ejecutando, también elimina el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="af8bb-163">Si elimina un trabajo que se ha completado correctamente o en caso contrario, elimina la información sobre el trabajo de hello completamente.</span><span class="sxs-lookup"><span data-stu-id="af8bb-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="af8bb-164">Uso de Livy Spark en clústeres de HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="af8bb-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="af8bb-165">Clúster de HDInsight 3.5, de forma predeterminada, deshabilita el uso de archivos de datos de ejemplo de tooaccess de rutas de acceso de archivo local o archivos JAR.</span><span class="sxs-lookup"><span data-stu-id="af8bb-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="af8bb-166">Le recomendamos que toouse hello `wasb://` ruta de acceso en su lugar archivos JAR tooaccess archivos o datos de ejemplo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="af8bb-167">Si desea toouse la ruta de acceso local, debe actualizar la configuración de Ambari de hello en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="af8bb-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="af8bb-168">toodo para:</span><span class="sxs-lookup"><span data-stu-id="af8bb-168">toodo so:</span></span>

1. <span data-ttu-id="af8bb-169">Vaya toohello Ambari portal para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="af8bb-170">Hola interfaz de usuario de Ambari Web está disponible en el clúster de HDInsight en https://**CLUSTERNAME**. azurehdidnsight.net, donde CLUSTERNAME es nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="af8bb-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="af8bb-171">En la barra de navegación izquierda de hello, haga clic en **Livio**y, a continuación, haga clic en **configuraciones**.</span><span class="sxs-lookup"><span data-stu-id="af8bb-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="af8bb-172">En **Livio predeterminado** Agregar nombre de la propiedad de hello `livy.file.local-dir-whitelist` y establezca su valor demasiado**"/"** si desea que el sistema de toofile de tooallow acceso completo.</span><span class="sxs-lookup"><span data-stu-id="af8bb-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="af8bb-173">Si desea que el directorio específico de tooallow acceso tooa solo, especifica el directorio de toothat de ruta de acceso de hello como valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="af8bb-174">Envío de trabajos de Livy para un clúster en una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="af8bb-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="af8bb-175">Si se conecta tooan clúster de HDInsight Spark desde dentro de una red Virtual de Azure, puede conectar directamente tooLivy en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="af8bb-176">En tal caso, Hola dirección URL de extremo Livio es `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="af8bb-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="af8bb-177">En este caso, **8998** es el puerto de Hola donde Livio se ejecuta en el nodo principal del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="af8bb-178">Para más información sobre el acceso a los servicios en puertos no públicos, vea [Puertos utilizados por los servicios Hadoop en HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="af8bb-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="af8bb-179">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="af8bb-179">Troubleshooting</span></span>

<span data-ttu-id="af8bb-180">Estas son algunas causas que pueden surgir al usar Livio para clústeres de tooSpark de envío de trabajo remoto.</span><span class="sxs-lookup"><span data-stu-id="af8bb-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="af8bb-181">No se admite el uso de un jar externo de almacenamiento adicional de Hola</span><span class="sxs-lookup"><span data-stu-id="af8bb-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="af8bb-182">**Problema:** si su trabajo Livio Spark hace referencia a un archivo jar externo de cuenta de almacenamiento adicional de hello asociada con el clúster de hello, se produce un error en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="af8bb-183">**Solución:** Asegúrese de que ese jar Hola desea toouse está disponible en almacenamiento de hello predeterminado asociado con el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="af8bb-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="af8bb-184">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="af8bb-184">Next step</span></span>

* [<span data-ttu-id="af8bb-185">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="af8bb-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="af8bb-186">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="af8bb-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

