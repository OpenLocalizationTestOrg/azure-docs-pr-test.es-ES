---
title: Uso de Pig en Hadoop con REST en HDInsight (Azure) | Microsoft Docs
description: "Aprenda a usar REST para ejecutar trabajos de Pig Latin en un clúster de Hadoop en Azure HDInsight."
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
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="1e6a1-103">Ejecución de trabajos de Pig con Hadoop en HDInsight con REST</span><span class="sxs-lookup"><span data-stu-id="1e6a1-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="1e6a1-104">Aprenda a ejecutar trabajos de Pig Latin mediante la creación de solicitudes de REST a un clúster de Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="1e6a1-105">Curl se usa para demostrar cómo puede interactuar con HDInsight mediante la API de REST WebHCat.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="1e6a1-106">Si ya está familiarizado con el uso de servidores de Hadoop basados en Linux, pero no conoce HDInsight, consulte [Información sobre el uso de HDInsight en Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="1e6a1-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="1e6a1-107"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e6a1-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="1e6a1-108">Un clúster de HDInsight de Azure (Hadoop en HDInsight) (basado en Windows o en Linux)</span><span class="sxs-lookup"><span data-stu-id="1e6a1-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1e6a1-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1e6a1-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1e6a1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="1e6a1-111">Curl</span><span class="sxs-lookup"><span data-stu-id="1e6a1-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="1e6a1-112">jq</span><span class="sxs-lookup"><span data-stu-id="1e6a1-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="1e6a1-113"><a id="curl"></a>Ejecución de trabajos de Pig con Curl</span><span class="sxs-lookup"><span data-stu-id="1e6a1-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="1e6a1-114">La API de REST se protege con la [autenticación de acceso básico](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="1e6a1-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="1e6a1-115">Para garantizar que las credenciales se envían de manera segura al servidor, siempre debe crear solicitudes usando HTTP segura (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="1e6a1-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="1e6a1-116">Cuando se usen los comandos de esta sección, reemplace `USERNAME` por el usuario para autenticación en el clúster y `PASSWORD` por la contraseña de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="1e6a1-117">Reemplace `CLUSTERNAME` por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="1e6a1-118">Desde una línea de comandos, utilice el siguiente comando para comprobar que puede conectarse al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="1e6a1-119">Recibirá la siguientes respuesta JSON:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="1e6a1-120">Los parámetros que se utilizan en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="1e6a1-121">**-u**: el nombre de usuario y la contraseña que se utilizan para autenticar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="1e6a1-122">**-G**: indica que esta es una solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="1e6a1-123">El comienzo del identificador URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será el mismo para todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="1e6a1-124">La ruta de acceso, **/status**, indica que la solicitud debe devolver el estado de WebHCat (también conocido como Templeton) al servidor.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="1e6a1-125">Utilice el siguiente código para enviar un trabajo de Pig Latin al clúster:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="1e6a1-126">Los parámetros que se utilizan en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="1e6a1-127">**-d**: como `-G` no se usa, la solicitud establece como valor predeterminado el método POST.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="1e6a1-128">`-d` especifica los valores de datos que se envían con la solicitud.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="1e6a1-129">**user.name**: el usuario que ejecuta el comando.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="1e6a1-130">**execute**: las instrucciones de Pig Latin que se ejecutarán.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="1e6a1-131">**statusdir**: el directorio donde se escribe el estado de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e6a1-132">Observe que los espacios en las instrucciones de Pig Latin se reemplazan por el carácter `+` cuando se utilizan con Curl.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="1e6a1-133">Este comando debe devolver un identificador de trabajo que se pueda usar para comprobar el estado del trabajo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="1e6a1-134">Para revisar el estado del trabajo, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="1e6a1-135">Reemplace `JOBID` por el valor devuelto en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="1e6a1-136">Por ejemplo, si el valor devuelto fue `{"id":"job_1415651640909_0026"}`, entonces `JOBID` es `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="1e6a1-137">Si se ha completado el trabajo, el estado es **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1e6a1-138">Esta solicitud de Curl devuelve un documento de notación de objetos JavaScript (JSON) con información acerca del trabajo; jq se usa para recuperar solo el valor de estado.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="1e6a1-139"><a id="results"></a>Visualización de resultados</span><span class="sxs-lookup"><span data-stu-id="1e6a1-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="1e6a1-140">Cuando el estado del trabajo haya cambiado a **SUCCEEDED**, puede recuperar los resultados del trabajo.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="1e6a1-141">El parámetro `statusdir` pasado con la consulta contiene la ubicación del archivo de salida; en este caso, `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="1e6a1-142">HDInsight puede usar Azure Storage o Azure Data Lake Store como almacén de datos predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="1e6a1-143">Hay varias maneras de obtener los datos, en función de la que use.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="1e6a1-144">Para más información, consulte la sección sobre almacenamiento del documento [Información sobre el uso de HDInsight en Linux](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="1e6a1-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="1e6a1-145"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="1e6a1-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="1e6a1-146">Como se muestra en este documento, puede utilizar la solicitud HTTP sin procesar para ejecutar, supervisar y ver los resultados de los trabajos de Hive en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e6a1-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="1e6a1-147">Para obtener más información sobre la interfaz REST utilizada en este artículo, consulte la [referencia de WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="1e6a1-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="1e6a1-148"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e6a1-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="1e6a1-149">Para obtener información general sobre Pig en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="1e6a1-150">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e6a1-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="1e6a1-151">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1e6a1-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1e6a1-152">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e6a1-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1e6a1-153">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="1e6a1-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
