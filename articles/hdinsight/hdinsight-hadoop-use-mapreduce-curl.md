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
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="675fe-103">Ejecución de trabajos de MapReduce con Hadoop en HDInsight con REST</span><span class="sxs-lookup"><span data-stu-id="675fe-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="675fe-104">Obtenga información acerca de cómo trabajos toouse Hola API de REST de WebHCat toorun MapReduce en un Hadoop en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="675fe-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="675fe-105">CURL es usado toodemonstrate cómo pueden interactuar con HDInsight mediante trabajos de MapReduce de toorun de las solicitudes HTTP sin formato.</span><span class="sxs-lookup"><span data-stu-id="675fe-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="675fe-106">Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea hello [lo que necesita tooknow sobre basado en Linux, Hadoop en HDInsight](hdinsight-hadoop-linux-information.md) documento.</span><span class="sxs-lookup"><span data-stu-id="675fe-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="675fe-107"><a id="prereq"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="675fe-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="675fe-108">Un clúster de Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="675fe-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="675fe-109">Curl</span><span class="sxs-lookup"><span data-stu-id="675fe-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="675fe-110">jq</span><span class="sxs-lookup"><span data-stu-id="675fe-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="675fe-111"><a id="curl"></a>Ejecución de trabajos de MapReduce mediante Curl</span><span class="sxs-lookup"><span data-stu-id="675fe-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="675fe-112">Cuando usas Curl o cualquier otro tipo de comunicación REST con WebHCat, debe autenticar solicitudes de hello proporcionando la contraseña y nombre de usuario de administrador de clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="675fe-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="675fe-113">Debe usar el nombre del clúster de hello como parte del URI que es usado toosend Hola solicitudes toohello servidor hello.</span><span class="sxs-lookup"><span data-stu-id="675fe-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="675fe-114">Para los comandos de hello en esta sección, reemplace **nombre de usuario** con clúster de hello usuario tooauthenticate toohello, y **contraseña** con contraseña hello para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="675fe-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="675fe-115">Reemplace **CLUSTERNAME** con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="675fe-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="675fe-116">Hello API de REST se protege utilizando [autenticación de acceso básico](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="675fe-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="675fe-117">Siempre debe realizar las solicitudes mediante tooensure HTTPS que sus credenciales se envían de forma segura toohello server.</span><span class="sxs-lookup"><span data-stu-id="675fe-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="675fe-118">Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:</span><span class="sxs-lookup"><span data-stu-id="675fe-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="675fe-119">Debería recibir un toohello similar de respuesta después de JSON:</span><span class="sxs-lookup"><span data-stu-id="675fe-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="675fe-120">parámetros de Hello utilizados en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="675fe-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="675fe-121">**-u**: indica Hola nombre de usuario y una contraseña usan solicitud de hello tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="675fe-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="675fe-122">**-G**: indica que esta operación es una solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="675fe-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="675fe-123">Hola a partir de hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Hola iguales para todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="675fe-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="675fe-124">toosubmit un trabajo MapReduce, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="675fe-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="675fe-125">final de Hola de hello URI (/ mapreduce/jar) indica WebHCat que esta solicitud inicia un trabajo de MapReduce desde una clase en un archivo jar.</span><span class="sxs-lookup"><span data-stu-id="675fe-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="675fe-126">parámetros de Hello utilizados en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="675fe-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="675fe-127">**-d**: `-G` no se utiliza, por lo que la solicitud de hello tiene como valor predeterminado el método POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="675fe-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="675fe-128">`-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="675fe-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="675fe-129">**User.nombre**: usuario de Hola que está ejecutando el comando hello</span><span class="sxs-lookup"><span data-stu-id="675fe-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="675fe-130">**JAR**: ubicación de hello del archivo jar de Hola que contiene la clase toobe se ejecutó</span><span class="sxs-lookup"><span data-stu-id="675fe-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="675fe-131">**clase**: Hola clase que contiene la lógica de MapReduce Hola</span><span class="sxs-lookup"><span data-stu-id="675fe-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="675fe-132">**arg**: Hola argumentos toobe pasa toohello trabajo de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="675fe-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="675fe-133">En este caso, Hola de entrada de directorio de hello y archivo de texto que se usa para la salida de hello</span><span class="sxs-lookup"><span data-stu-id="675fe-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="675fe-134">Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="675fe-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="675fe-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="675fe-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="675fe-136">estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="675fe-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="675fe-137">Reemplace hello **JOBID** con valor Hola devuelta en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="675fe-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="675fe-138">Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, Hola JOBID sería `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="675fe-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="675fe-139">Si el trabajo de hello está completado, el estado de hello devuelto es `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="675fe-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="675fe-140">Esta solicitud Curl devuelve un documento JSON con información sobre el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="675fe-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="675fe-141">Se utiliza Jq tooretrieve Hola solo el valor de estado.</span><span class="sxs-lookup"><span data-stu-id="675fe-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="675fe-142">Cuando el estado de Hola de trabajo de hello ha cambiado demasiado`SUCCEEDED`, se pueden recuperar resultados de Hola de trabajo de Hola desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="675fe-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="675fe-143">Hola `statusdir` parámetro que se pasa con la consulta de hello contiene la ubicación de Hola Hola del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="675fe-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="675fe-144">En este ejemplo, la ubicación de hello es `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="675fe-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="675fe-145">Esta dirección almacena los resultados de Hola de trabajo de hello en almacenamiento de hello clústeres predeterminado en `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="675fe-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="675fe-146">Puede enumerar y descargar estos archivos mediante el uso de hello [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="675fe-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="675fe-147">Para obtener más información sobre cómo trabajar con blobs de hello CLI de Azure, vea hello [hello mediante Azure CLI 2.0 con el almacenamiento de Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) documento.</span><span class="sxs-lookup"><span data-stu-id="675fe-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="675fe-148"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="675fe-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="675fe-149">Para obtener información general sobre los trabajos de MapReduce en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="675fe-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="675fe-150">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="675fe-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="675fe-151">Para obtener información sobre otras maneras de trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="675fe-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="675fe-152">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="675fe-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="675fe-153">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="675fe-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="675fe-154">Para obtener más información acerca de la interfaz REST de Hola que se usa en este artículo, consulte hello [WebHCat referencia](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="675fe-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
