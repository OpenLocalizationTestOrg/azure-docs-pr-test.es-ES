---
title: Uso de Sqoop en Hadoop con Curl en HDInsight (Azure)| Microsoft Docs
description: "Obtenga información sobre cómo enviar remotamente trabajos a HDInsight usando Curl."
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
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="0613f-103">Ejecución de trabajos de Sqoop con Hadoop en HDInsight con Curl</span><span class="sxs-lookup"><span data-stu-id="0613f-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="0613f-104">En este documento aprenderá a utilizar Curl para ejecutar trabajos de Sqoop en un clúster de Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0613f-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="0613f-105">Curl sirve para demostrar cómo se puede interactuar con HDInsight usando solicitudes HTTP sin procesar para ejecutar, supervisar y recuperar los resultados de los trabajos de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="0613f-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="0613f-106">Esto funciona mediante la API de REST de WebHCat (conocida anteriormente como Templeton) proporcionada por el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0613f-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="0613f-107">Si ya está familiarizado con el uso de servidores de Hadoop basados en Linux, pero no conoce HDInsight, consulte [Información sobre el uso de HDInsight en Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="0613f-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0613f-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0613f-108">Prerequisites</span></span>
<span data-ttu-id="0613f-109">Para completar los pasos de este artículo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0613f-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="0613f-110">Un clúster de Hadoop en HDInsight (basado en Linux o Windows)</span><span class="sxs-lookup"><span data-stu-id="0613f-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="0613f-111">Curl</span><span class="sxs-lookup"><span data-stu-id="0613f-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="0613f-112">jq</span><span class="sxs-lookup"><span data-stu-id="0613f-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="0613f-113">Envío de trabajos de Sqoop mediante Curl</span><span class="sxs-lookup"><span data-stu-id="0613f-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="0613f-114">Al usar Curl o cualquier otra comunicación REST con WebHCat, debe proporcionar el nombre de usuario y la contraseña del administrador del clúster de HDInsight para autenticar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="0613f-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="0613f-115">También debe usar el nombre del clúster como parte del identificador uniforme de recursos (URI) que se usa para enviar las solicitudes al servidor.</span><span class="sxs-lookup"><span data-stu-id="0613f-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="0613f-116">En el caso de los comandos que aparecen en esta sección, reemplace **USERNAME** por el usuario para autenticación en el clúster y **PASSWORD** por la contraseña de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="0613f-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="0613f-117">Reemplace **CLUSTERNAME** por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="0613f-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="0613f-118">La API de REST se protege con la [autenticación básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="0613f-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="0613f-119">Siempre debe crear solicitudes usando HTTP segura (HTTPS) para así garantizar que las credenciales se envían de manera segura al servidor.</span><span class="sxs-lookup"><span data-stu-id="0613f-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="0613f-120">Desde una línea de comandos, utilice el siguiente comando para comprobar que puede conectarse al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0613f-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="0613f-121">Debería recibir una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0613f-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="0613f-122">Los parámetros que se utilizan en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="0613f-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="0613f-123">**-u** : el nombre de usuario y la contraseña que se utilizan para autenticar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0613f-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="0613f-124">**-G** : indica que esta es una solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="0613f-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="0613f-125">El principio de la dirección URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será el mismo para todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="0613f-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="0613f-126">La ruta de acceso, **/status**, indica que la solicitud debe devolver un estado de WebHCat (también conocido como Templeton) al servidor.</span><span class="sxs-lookup"><span data-stu-id="0613f-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="0613f-127">Para enviar el trabajo de sqoop, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0613f-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="0613f-128">Los parámetros que se utilizan en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="0613f-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="0613f-129">**-d**: como `-G` no se usa, la solicitud establece como valor predeterminado el método POST.</span><span class="sxs-lookup"><span data-stu-id="0613f-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="0613f-130">`-d` especifica los valores de datos que se envían con la solicitud.</span><span class="sxs-lookup"><span data-stu-id="0613f-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="0613f-131">**user.name** : el usuario que ejecuta el comando.</span><span class="sxs-lookup"><span data-stu-id="0613f-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="0613f-132">**command** : el comando de Sqoop para ejecutar.</span><span class="sxs-lookup"><span data-stu-id="0613f-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="0613f-133">**statusdir** : el directorio donde se escribirá el estado de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="0613f-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="0613f-134">Este comando debe devolver un identificador de trabajo que se pueda usar para comprobar el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="0613f-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="0613f-135">Para revisar el estado del trabajo, use el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0613f-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="0613f-136">Reemplace **JOBID** por el valor devuelto en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="0613f-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="0613f-137">Por ejemplo, si el valor devuelto fuese `{"id":"job_1415651640909_0026"}`, entonces **JOBID** sería `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="0613f-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="0613f-138">Si se completó el trabajo, el estado será **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="0613f-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0613f-139">Esta solicitud de Curl devuelve un documento de notación de objetos JavaScript (JSON) con información acerca del trabajo; jq se usa para recuperar solo el valor de estado.</span><span class="sxs-lookup"><span data-stu-id="0613f-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="0613f-140">Una vez que el estado del trabajo cambió a **SUCCEEDED**, puede recuperar los resultados del trabajo desde Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0613f-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="0613f-141">El parámetro `statusdir` transmitido con la consulta contiene la ubicación del archivo de salida; en este caso, **wasb:///example/curl**.</span><span class="sxs-lookup"><span data-stu-id="0613f-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="0613f-142">Esta dirección almacena la salida del trabajo en el directorio **example/curl** en el contenedor de almacenamiento predeterminado que su clúster de HDInsight usa.</span><span class="sxs-lookup"><span data-stu-id="0613f-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="0613f-143">Puede enumerar y descargar estos archivos mediante la [CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0613f-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="0613f-144">Por ejemplo, para enumerar los archivos existentes en **example/curl**, use el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0613f-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="0613f-145">Para descargar un archivo, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0613f-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="0613f-146">Debe especificar el nombre de la cuenta de almacenamiento que contiene el blob usando los parámetros `-a` y `-k` o bien, definir las variables de entorno **AZURE\_STORAGE\_ACCOUNT** y **AZURE\_STORAGE\_ACCESS\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="0613f-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="0613f-147">Vea <a href="hdinsight-upload-data.md" target="_blank" para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0613f-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="0613f-148">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="0613f-148">Limitations</span></span>
* <span data-ttu-id="0613f-149">Exportación masiva: con HDInsight basado en Linux, el conector Sqoop que se utiliza para exportar datos a Microsoft SQL Server o Base de datos SQL Azure no es compatible actualmente con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="0613f-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="0613f-150">Procesamiento por lotes: con HDInsight basado en Linux, cuando se usa `-batch` al realizar inserciones, Sqoop realizará varias inserciones en lugar de procesar por lotes las operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="0613f-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="0613f-151">Resumen</span><span class="sxs-lookup"><span data-stu-id="0613f-151">Summary</span></span>
<span data-ttu-id="0613f-152">Tal como se ha mostrado en este documento, puede usar una solicitud HTTP sin procesar para ejecutar, supervisar y ver los resultados de los trabajos de Sqoop en su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0613f-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="0613f-153">Para obtener más información sobre la interfaz REST utilizada en este artículo, consulte la referencia <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API Guide</a>.</span><span class="sxs-lookup"><span data-stu-id="0613f-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0613f-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0613f-154">Next steps</span></span>
<span data-ttu-id="0613f-155">Si desea obtener información general sobre Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0613f-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="0613f-156">Uso de Sqoop con Hadoop en HDInsight (Windows)</span><span class="sxs-lookup"><span data-stu-id="0613f-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="0613f-157">Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0613f-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="0613f-158">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0613f-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0613f-159">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0613f-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0613f-160">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0613f-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


