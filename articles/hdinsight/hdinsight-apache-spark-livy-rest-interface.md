---
title: "Uso de Livy Spark para enviar trabajos a un clúster Spark de Azure HDInsight | Microsoft Docs"
description: "Obtenga información sobre cómo usar la API de REST de Apache Spark para enviar trabajos de Spark de forma remota a un clúster de Azure HDInsight."
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
ms.openlocfilehash: e1a28d69bbf40ea3134a7899a0d2fe70e5fc9e71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="021ac-104">Uso de la API de REST de Apache Spark para enviar trabajos remotos a un clúster Spark de HDInsight</span><span class="sxs-lookup"><span data-stu-id="021ac-104">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="021ac-105">Obtenga información sobre cómo usar Livy, la API de REST de Apache Spark, que se usa para enviar trabajos remotos a un clúster Spark de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="021ac-105">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="021ac-106">Para obtener documentación detallada, vea [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="021ac-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="021ac-107">Puede usar Livy para ejecutar shells de Spark interactivos o enviar trabajos por lotes que se ejecutarán en Spark.</span><span class="sxs-lookup"><span data-stu-id="021ac-107">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="021ac-108">Este artículo trata acerca de cómo utilizar Livy para enviar trabajos por lotes.</span><span class="sxs-lookup"><span data-stu-id="021ac-108">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="021ac-109">Los fragmentos de código de este artículo usan cURL para realizar llamadas de la API de REST al punto de conexión de Livy Spark.</span><span class="sxs-lookup"><span data-stu-id="021ac-109">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="021ac-110">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="021ac-110">**Prerequisites:**</span></span>

* <span data-ttu-id="021ac-111">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="021ac-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="021ac-112">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="021ac-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="021ac-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="021ac-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="021ac-114">En este artículo se usa cURL para mostrar cómo realizar llamadas de la API de REST a un clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="021ac-114">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="021ac-115">Envío de un trabajo por lotes de Livy Spark</span><span class="sxs-lookup"><span data-stu-id="021ac-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="021ac-116">Antes de enviar un trabajo por lotes, debe cargar el archivo jar de aplicación en el almacenamiento del clúster asociado al clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="021ac-117">Puede usar [**AzCopy**](../storage/common/storage-use-azcopy.md), una utilidad de línea de comandos, para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="021ac-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="021ac-118">Hay muchos otros clientes que se pueden usar para cargar datos.</span><span class="sxs-lookup"><span data-stu-id="021ac-118">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="021ac-119">Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="021ac-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="021ac-120">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="021ac-120">**Examples**:</span></span>

* <span data-ttu-id="021ac-121">Si el archivo jar se encuentra en el almacenamiento de clúster (WASB)</span><span class="sxs-lookup"><span data-stu-id="021ac-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="021ac-122">Si quiere pasar el nombre del archivo jar y el nombre de clase como parte de un archivo de entrada (en este ejemplo, input.txt)</span><span class="sxs-lookup"><span data-stu-id="021ac-122">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="021ac-123">Obtención de información sobre los lotes de Livy Spark que se ejecutan en el clúster</span><span class="sxs-lookup"><span data-stu-id="021ac-123">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="021ac-124">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="021ac-124">**Examples**:</span></span>

* <span data-ttu-id="021ac-125">Si desea recuperar todos los lotes de Livy Spark que se ejecutan en el clúster:</span><span class="sxs-lookup"><span data-stu-id="021ac-125">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="021ac-126">Si desea recuperar un lote específico con un determinado identificador de lote</span><span class="sxs-lookup"><span data-stu-id="021ac-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="021ac-127">Eliminación de un trabajo por lotes de Livy Spark</span><span class="sxs-lookup"><span data-stu-id="021ac-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="021ac-128">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="021ac-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="021ac-129">Livy Spark y alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="021ac-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="021ac-130">Livy proporciona alta disponibilidad para los trabajos de Spark que se ejecuten en el clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="021ac-131">Estos son algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="021ac-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="021ac-132">Si el servicio Livy deja de funcionar después de haber enviado un trabajo de forma remota a un clúster Spark, dicho trabajo continúa ejecutándose en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="021ac-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="021ac-133">Cuando se restablece el funcionamiento de Livy, restaura el estado del trabajo e informa de ello.</span><span class="sxs-lookup"><span data-stu-id="021ac-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="021ac-134">Los cuadernos de Jupyter Notebook para HDInsight cuentan con la tecnología de Livy en el backend.</span><span class="sxs-lookup"><span data-stu-id="021ac-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="021ac-135">Si un cuaderno ejecuta un trabajo de Spark y se reinicia el servicio Livy, el cuaderno sigue ejecutando las celdas de código.</span><span class="sxs-lookup"><span data-stu-id="021ac-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="021ac-136">Mostrar un ejemplo</span><span class="sxs-lookup"><span data-stu-id="021ac-136">Show me an example</span></span>
<span data-ttu-id="021ac-137">En esta sección se verán ejemplos de uso de Livy Spark para enviar un trabajo por lotes, supervisar el progreso del trabajo y después eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="021ac-137">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="021ac-138">La aplicación que se usa en este ejemplo es la que se desarrolla en el artículo [Creación de una aplicación de Scala independiente para ejecutarla en el clúster HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="021ac-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="021ac-139">En los pasos siguientes se da por hecho que:</span><span class="sxs-lookup"><span data-stu-id="021ac-139">The steps here assume that:</span></span>

* <span data-ttu-id="021ac-140">Ya ha copiado el archivo JAR de la aplicación en la cuenta de almacenamiento asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="021ac-141">Tiene CuRL instalado en el equipo donde intenta seguir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="021ac-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="021ac-142">Lleve a cabo los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="021ac-142">Perform the following steps:</span></span>

1. <span data-ttu-id="021ac-143">Nos gustaría comprobar primero que Livy Spark se está ejecutando en el clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-143">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="021ac-144">Podemos hacerlo mediante la obtención de una lista de lotes en ejecución.</span><span class="sxs-lookup"><span data-stu-id="021ac-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="021ac-145">Si es la primera vez que ejecuta un trabajo con Livy, la salida debe devolver cero.</span><span class="sxs-lookup"><span data-stu-id="021ac-145">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="021ac-146">Debería obtener una salida similar al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="021ac-146">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="021ac-147">Observe que la última línea de la salida indica **total: 0**, lo que sugiere que no hay lotes en ejecución.</span><span class="sxs-lookup"><span data-stu-id="021ac-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="021ac-148">Ahora vamos a enviar un trabajo por lotes.</span><span class="sxs-lookup"><span data-stu-id="021ac-148">Let us now submit a batch job.</span></span> <span data-ttu-id="021ac-149">El fragmento de código siguiente usa un archivo de entrada (input.txt) para pasar el nombre del archivo jar y el nombre de clase como parámetros.</span><span class="sxs-lookup"><span data-stu-id="021ac-149">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="021ac-150">Si ejecuta estos pasos desde un equipo Windows, el enfoque recomendado es usar un archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="021ac-150">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="021ac-151">A continuación se definen los parámetros del archivo **input.txt** :</span><span class="sxs-lookup"><span data-stu-id="021ac-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="021ac-152">Debería ver una salida similar al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="021ac-152">You should see an output similar to the  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="021ac-153">Observe que la última línea del resultado indica **state:starting**.</span><span class="sxs-lookup"><span data-stu-id="021ac-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="021ac-154">También indica **id:0**.</span><span class="sxs-lookup"><span data-stu-id="021ac-154">It also says, **id:0**.</span></span> <span data-ttu-id="021ac-155">Aquí, **0** es el identificador de lote.</span><span class="sxs-lookup"><span data-stu-id="021ac-155">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="021ac-156">Ahora puede recuperar el estado de este lote concreto con el identificador de lote.</span><span class="sxs-lookup"><span data-stu-id="021ac-156">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="021ac-157">Debería ver una salida similar al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="021ac-157">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="021ac-158">La salida muestra ahora **state:success**, lo que sugiere que el trabajo se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="021ac-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="021ac-159">Si lo desea, ahora puede eliminar el lote.</span><span class="sxs-lookup"><span data-stu-id="021ac-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="021ac-160">Debería ver una salida similar al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="021ac-160">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="021ac-161">La última línea de la salida indica que el lote se ha eliminado correctamente.</span><span class="sxs-lookup"><span data-stu-id="021ac-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="021ac-162">Al eliminar un trabajo mientras se está ejecutando también se termina.</span><span class="sxs-lookup"><span data-stu-id="021ac-162">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="021ac-163">Si elimina un trabajo que se ha completado correctamente o incorrectamente, elimina la información del trabajo por completo.</span><span class="sxs-lookup"><span data-stu-id="021ac-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="021ac-164">Uso de Livy Spark en clústeres de HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="021ac-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="021ac-165">Un clúster de HDInsight 3.5 deshabilita de forma predeterminada el uso de rutas de acceso a archivos locales para el acceso a archivos de datos de ejemplo o archivos jar.</span><span class="sxs-lookup"><span data-stu-id="021ac-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="021ac-166">Le recomendamos que use la ruta de acceso `wasb://` en su lugar para tener acceso a archivos jar o archivos de datos de ejemplo desde el clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="021ac-167">Si desea usar la ruta de acceso local, debe actualizar la configuración de Ambari en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="021ac-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="021ac-168">Para ello:</span><span class="sxs-lookup"><span data-stu-id="021ac-168">To do so:</span></span>

1. <span data-ttu-id="021ac-169">Vaya al portal de Ambari para el clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="021ac-170">La interfaz de usuario web de Ambari está disponible en el clúster de HDInsight en https://**CLUSTERNAME**.azurehdidnsight.net, donde CLUSTERNAME es el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="021ac-171">En el panel de navegación izquierdo, haga clic en **Livy**y, a continuación, haga clic en **Configs** (Configuraciones).</span><span class="sxs-lookup"><span data-stu-id="021ac-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="021ac-172">En **livy-default**, agregue el nombre de propiedad `livy.file.local-dir-whitelist` y establezca su valor en **"/"** si desea permitir el acceso total al sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="021ac-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="021ac-173">Si desea permitir el acceso únicamente a un directorio específico, proporcione la ruta de acceso a ese directorio como valor.</span><span class="sxs-lookup"><span data-stu-id="021ac-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="021ac-174">Envío de trabajos de Livy para un clúster en una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="021ac-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="021ac-175">Si se conecta a un clúster de HDInsight Spark desde una red virtual de Azure, puede conectarse directamente a Livy en el clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-175">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="021ac-176">En tal caso, la dirección URL del punto de conexión de Livy es `http://<IP address of the headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="021ac-176">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="021ac-177">Aquí, **8998** es el puerto en el que se ejecuta Livy en el nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="021ac-177">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="021ac-178">Para más información sobre el acceso a los servicios en puertos no públicos, vea [Puertos utilizados por los servicios Hadoop en HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="021ac-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="021ac-179">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="021ac-179">Troubleshooting</span></span>

<span data-ttu-id="021ac-180">Estos son algunos de los problemas que pueden surgir a la hora de utilizar Livy para el envío de trabajo remoto a clústeres de Spark.</span><span class="sxs-lookup"><span data-stu-id="021ac-180">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="021ac-181">No se admite el uso de un archivo jar externo desde el almacenamiento adicional</span><span class="sxs-lookup"><span data-stu-id="021ac-181">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="021ac-182">**Problema**: si el trabajo de Livy Spark hace referencia a un archivo .jar externo de la cuenta de almacenamiento adicional asociada al clúster, se produce un error en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="021ac-182">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="021ac-183">**Solución:** asegúrese de que el archivo jar que desea usar se encuentra disponible en el almacenamiento predeterminado asociado al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="021ac-183">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="021ac-184">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="021ac-184">Next step</span></span>

* [<span data-ttu-id="021ac-185">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="021ac-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="021ac-186">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="021ac-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

