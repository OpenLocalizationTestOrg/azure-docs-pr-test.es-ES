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
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="d5221-103">Ejecución de trabajos de Pig con Hadoop en HDInsight con REST</span><span class="sxs-lookup"><span data-stu-id="d5221-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="d5221-104">Obtenga información acerca de cómo toorun Pig latino trabajos mediante la realización de clúster de HDInsight de Azure de tooan de las solicitudes REST.</span><span class="sxs-lookup"><span data-stu-id="d5221-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="d5221-105">CURL es usado toodemonstrate cómo pueden interactuar con HDInsight con la API de REST de WebHCat Hola.</span><span class="sxs-lookup"><span data-stu-id="d5221-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="d5221-106">Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea [sugerencias de HDInsight basados en Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="d5221-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="d5221-107"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d5221-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="d5221-108">Un clúster de HDInsight de Azure (Hadoop en HDInsight) (basado en Windows o en Linux)</span><span class="sxs-lookup"><span data-stu-id="d5221-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d5221-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="d5221-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d5221-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d5221-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="d5221-111">Curl</span><span class="sxs-lookup"><span data-stu-id="d5221-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="d5221-112">jq</span><span class="sxs-lookup"><span data-stu-id="d5221-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="d5221-113"><a id="curl"></a>Ejecución de trabajos de Pig con Curl</span><span class="sxs-lookup"><span data-stu-id="d5221-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="d5221-114">API de REST de Hello se protege una a través de [autenticación de acceso básico](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="d5221-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="d5221-115">Siempre se realizan las solicitudes mediante el uso de tooensure HTTP seguro (HTTPS) que sus credenciales se envían de forma segura toohello server.</span><span class="sxs-lookup"><span data-stu-id="d5221-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="d5221-116">Cuando utilice comandos de hello en esta sección, reemplace `USERNAME` por clúster de hello usuario tooauthenticate toohello y `PASSWORD` con la contraseña de hello para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5221-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="d5221-117">Reemplace `CLUSTERNAME` con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="d5221-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="d5221-118">Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:</span><span class="sxs-lookup"><span data-stu-id="d5221-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="d5221-119">Debería recibir Hola después de la respuesta JSON:</span><span class="sxs-lookup"><span data-stu-id="d5221-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="d5221-120">parámetros de Hello utilizados en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5221-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="d5221-121">**-u**: Hola nombre de usuario y la contraseña utilizan la solicitud de hello tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="d5221-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="d5221-122">**-G**: indica que esta es una solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="d5221-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="d5221-123">Hola a partir de la dirección URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Hola iguales para todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="d5221-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="d5221-124">ruta de acceso de Hello, **/Status**, indica esa solicitud hello es el estado de hello tooreturn WebHCat (también conocido como Templeton) para servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5221-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="d5221-125">Usar hello después de un clúster de toohello de trabajo de Pig latino del código toosubmit:</span><span class="sxs-lookup"><span data-stu-id="d5221-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="d5221-126">parámetros de Hello utilizados en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5221-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="d5221-127">**-d**: porque `-G` no se utiliza, solicitud de hello tiene como valor predeterminado el método POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="d5221-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="d5221-128">`-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="d5221-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="d5221-129">**User.nombre**: usuario de Hola que está ejecutando el comando hello</span><span class="sxs-lookup"><span data-stu-id="d5221-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="d5221-130">**ejecutar**: Hola Pig latino instrucciones tooexecute</span><span class="sxs-lookup"><span data-stu-id="d5221-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="d5221-131">**statusdir**: se escribió en el directorio de Hola que Hola estado para este trabajo</span><span class="sxs-lookup"><span data-stu-id="d5221-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5221-132">Tenga en cuenta que los espacios de hello en las instrucciones de Pig latino se sustituyen con hello `+` caracteres cuando se usa con el doblez.</span><span class="sxs-lookup"><span data-stu-id="d5221-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="d5221-133">Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d5221-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="d5221-134">estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando</span><span class="sxs-lookup"><span data-stu-id="d5221-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="d5221-135">Reemplace `JOBID` con el valor de hello devuelta en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5221-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="d5221-136">Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, `JOBID` es `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="d5221-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="d5221-137">Si ha terminado el trabajo de hello, estado de hello es **correcto**.</span><span class="sxs-lookup"><span data-stu-id="d5221-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5221-138">Esta solicitud Curl devuelve un JavaScript Object Notation (JSON) de documentos con información sobre el trabajo de Hola y jq es tooretrieve usado Hola solo el valor de estado.</span><span class="sxs-lookup"><span data-stu-id="d5221-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="d5221-139"><a id="results"></a>Visualización de resultados</span><span class="sxs-lookup"><span data-stu-id="d5221-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="d5221-140">Cuando el estado de Hola de trabajo de hello ha cambiado demasiado**correcto**, se pueden recuperar resultados de Hola de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5221-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="d5221-141">Hola `statusdir` parámetro pasado con hello consulta contiene ubicación de Hola Hola del archivo de salida; en este caso, `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="d5221-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="d5221-142">HDInsight puede usar el almacenamiento de Azure o almacén de Azure Data Lake como almacén de datos predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5221-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="d5221-143">No hay tooget de varias maneras en datos Hola dependiendo de cuál utilizar.</span><span class="sxs-lookup"><span data-stu-id="d5221-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="d5221-144">Para obtener más información, vea la sección de almacenamiento de Hola de hello [información de HDInsight basados en Linux](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) documento.</span><span class="sxs-lookup"><span data-stu-id="d5221-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="d5221-145"><a id="summary"></a>Resumen</span><span class="sxs-lookup"><span data-stu-id="d5221-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="d5221-146">Como se muestra en este documento, puede usar un toorun de solicitud HTTP sin formato, al monitor y ver los resultados de los trabajos de Pig hello en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5221-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="d5221-147">Para obtener más información acerca de la interfaz REST de hello usan en este artículo, consulte hello [WebHCat referencia](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="d5221-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="d5221-148"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5221-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="d5221-149">Para obtener información general sobre Pig en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d5221-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="d5221-150">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5221-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="d5221-151">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d5221-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d5221-152">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5221-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d5221-153">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5221-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
