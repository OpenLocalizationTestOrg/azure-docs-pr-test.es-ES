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
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="9770e-103">Ejecución de trabajos de Sqoop con Hadoop en HDInsight con Curl</span><span class="sxs-lookup"><span data-stu-id="9770e-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="9770e-104">Obtenga información acerca de cómo agrupar toouse Curl toorun Sqoop trabajos en un Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9770e-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="9770e-105">CURL es usado toodemonstrate cómo pueden interactuar con HDInsight mediante toorun de las solicitudes HTTP sin formato, monitor y recuperar los resultados de Hola de trabajos de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="9770e-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="9770e-106">Esto funciona con hello WebHCat REST API (anteriormente conocido como Templeton) proporcionado por el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9770e-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="9770e-107">Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea [información sobre el uso de HDInsight en Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="9770e-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9770e-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9770e-108">Prerequisites</span></span>
<span data-ttu-id="9770e-109">pasos de hello toocomplete en este artículo, se necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9770e-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="9770e-110">Un clúster de Hadoop en HDInsight (basado en Linux o Windows)</span><span class="sxs-lookup"><span data-stu-id="9770e-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="9770e-111">Curl</span><span class="sxs-lookup"><span data-stu-id="9770e-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="9770e-112">jq</span><span class="sxs-lookup"><span data-stu-id="9770e-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="9770e-113">Envío de trabajos de Sqoop mediante Curl</span><span class="sxs-lookup"><span data-stu-id="9770e-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="9770e-114">Al usar Curl o cualquier otro tipo de comunicación REST con WebHCat, debe autenticar solicitudes de hello proporcionando el nombre de usuario de Hola y la contraseña de administrador de clústeres de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="9770e-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="9770e-115">También debe usar el nombre del clúster de hello como parte del identificador uniforme de recursos (URI) de hello utiliza servidor toohello de toosend hello las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="9770e-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="9770e-116">Para los comandos de hello en esta sección, reemplace **nombre de usuario** por clúster de hello usuario tooauthenticate toohello y **contraseña** con contraseña hello para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9770e-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="9770e-117">Reemplace **CLUSTERNAME** con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="9770e-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="9770e-118">API de REST de Hello se protege una a través de [la autenticación básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="9770e-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="9770e-119">Siempre debe realizar las solicitudes mediante el uso de HTTP seguro (HTTPS) toohelp Asegúrese de que sus credenciales se envían de forma segura toohello server.</span><span class="sxs-lookup"><span data-stu-id="9770e-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="9770e-120">Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:</span><span class="sxs-lookup"><span data-stu-id="9770e-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="9770e-121">Debería recibir un siguiente toohello similar de respuesta:</span><span class="sxs-lookup"><span data-stu-id="9770e-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="9770e-122">parámetros de Hello utilizados en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9770e-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="9770e-123">**-u** -Hola nombre de usuario y una contraseña usan tooauthenticate solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="9770e-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="9770e-124">**-G** : indica que esta es una solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="9770e-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="9770e-125">Hola a partir de la dirección URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, será el mismo Hola para todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="9770e-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="9770e-126">ruta de acceso de Hello, **/Status**, indica esa solicitud hello es tooreturn un estado de WebHCat (también conocido como Templeton) para servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="9770e-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="9770e-127">Usar hello después de un trabajo de sqoop toosubmit:</span><span class="sxs-lookup"><span data-stu-id="9770e-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="9770e-128">parámetros de Hello utilizados en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9770e-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="9770e-129">**-d** : desde `-G` no se utiliza, solicitud de hello tiene como valor predeterminado el método POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="9770e-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="9770e-130">`-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="9770e-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="9770e-131">**User.nombre** -usuario Hola que se ejecuta el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="9770e-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="9770e-132">**comando** -Hola Sqoop comando tooexecute.</span><span class="sxs-lookup"><span data-stu-id="9770e-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="9770e-133">**statusdir** -directorio Hola Hola estado para este trabajo se escribirán en.</span><span class="sxs-lookup"><span data-stu-id="9770e-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="9770e-134">Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9770e-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="9770e-135">estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="9770e-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="9770e-136">Reemplace **JOBID** con valor Hola devuelta en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9770e-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="9770e-137">Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, **JOBID** sería `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="9770e-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="9770e-138">Si ha terminado el trabajo de hello, estado de hello será **correcto**.</span><span class="sxs-lookup"><span data-stu-id="9770e-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9770e-139">Esta solicitud Curl devuelve un documento de JavaScript Object Notation (JSON) con información sobre el trabajo de hello; se utiliza jq tooretrieve Hola solo el valor de estado.</span><span class="sxs-lookup"><span data-stu-id="9770e-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="9770e-140">Una vez que el estado de Hola de trabajo de hello ha cambiado demasiado**correcto**, se pueden recuperar resultados de Hola de trabajo de Hola desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9770e-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="9770e-141">Hola `statusdir` parámetro pasado con hello consulta contiene ubicación de Hola Hola del archivo de salida; en este caso, **wasb: / / / ejemplo/curl**.</span><span class="sxs-lookup"><span data-stu-id="9770e-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="9770e-142">Esta dirección almacena los resultados de Hola de trabajo de Hola Hola **ejemplo/curl** directorio en el contenedor de almacenamiento de hello predeterminado utilizado por el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9770e-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="9770e-143">Puede enumerar y descargar estos archivos mediante el uso de hello [CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9770e-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="9770e-144">Por ejemplo, archivos toolist en **ejemplo/curl**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9770e-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="9770e-145">toodownload un archivo, utilice la siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="9770e-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="9770e-146">O bien debe especificar el nombre de cuenta de almacenamiento de Hola que contiene datos de blob de hello mediante el uso de hello `-a` y `-k` parámetros o conjunto hello **AZURE\_almacenamiento\_cuenta** y **AZURE\_almacenamiento\_acceso\_clave** variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="9770e-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="9770e-147">Vea <a href="hdinsight-upload-data.md" target="_blank" para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9770e-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="9770e-148">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="9770e-148">Limitations</span></span>
* <span data-ttu-id="9770e-149">La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="9770e-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="9770e-150">Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop llevará a cabo varias inserciones en lugar de las operaciones de inserción de Hola de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="9770e-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="9770e-151">Resumen</span><span class="sxs-lookup"><span data-stu-id="9770e-151">Summary</span></span>
<span data-ttu-id="9770e-152">Como se muestra en este documento, puede usar un toorun de solicitud HTTP sin formato, al monitor y ver los resultados de los trabajos de Sqoop hello en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9770e-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="9770e-153">Para obtener más información sobre la interfaz REST de hello usan en este artículo, consulte hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Guía de la API de REST de Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="9770e-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9770e-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9770e-154">Next steps</span></span>
<span data-ttu-id="9770e-155">Si desea obtener información general sobre Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9770e-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="9770e-156">Uso de Sqoop con Hadoop en HDInsight (Windows)</span><span class="sxs-lookup"><span data-stu-id="9770e-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="9770e-157">Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9770e-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="9770e-158">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9770e-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9770e-159">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9770e-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9770e-160">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9770e-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


