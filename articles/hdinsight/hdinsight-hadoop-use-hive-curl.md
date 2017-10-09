---
title: aaaUse Hive de Hadoop con doblez en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo enviar tooremotely Pig trabajos tooHDInsight mediante Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="f29af-103">Ejecución de consultas de Hive con Hadoop en HDInsight con REST</span><span class="sxs-lookup"><span data-stu-id="f29af-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="f29af-104">Obtenga información acerca de cómo las consultas toouse Hola API de REST de WebHCat toorun Hive con Hadoop en clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="f29af-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="f29af-105">[CURL](http://curl.haxx.se/) es usado toodemonstrate cómo pueden interactuar con HDInsight mediante el uso de las solicitudes HTTP sin formato.</span><span class="sxs-lookup"><span data-stu-id="f29af-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="f29af-106">Hola [jq](http://stedolan.github.io/jq/) utilidad incluye datos JSON de hello tooprocess usado devueltos desde solicitudes REST.</span><span class="sxs-lookup"><span data-stu-id="f29af-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="f29af-107">Si ya está familiarizado con el uso de servidores basado en Linux, Hadoop, pero son tooHDInsight nueva, vea hello [lo que necesita tooknow acerca de Hadoop en HDInsight basados en Linux](hdinsight-hadoop-linux-information.md) documento.</span><span class="sxs-lookup"><span data-stu-id="f29af-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="f29af-108"><a id="curl"></a>Ejecución de consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="f29af-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="f29af-109">Al usar cURL o cualquier otro tipo de comunicación REST con WebHCat, debe autenticar solicitudes de hello proporcionando el nombre de usuario de Hola y la contraseña de administrador de clústeres de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="f29af-110">Para los comandos de hello en esta sección, reemplace **nombre de usuario** por clúster de hello usuario tooauthenticate toohello y **contraseña** con contraseña hello para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="f29af-111">Reemplace **CLUSTERNAME** con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="f29af-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="f29af-112">API de REST de Hello se protege una a través de [la autenticación básica](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="f29af-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="f29af-113">toohelp Asegúrese de que las credenciales de forma segura siempre envía toohello servidor, realizar solicitudes mediante HTTP seguro (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="f29af-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="f29af-114">Desde una línea de comandos, use Hola después tooverify de comando que se puede conectar el clúster de HDInsight de tooyour:</span><span class="sxs-lookup"><span data-stu-id="f29af-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="f29af-115">Recibirá un toohello similar de respuesta siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="f29af-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="f29af-116">parámetros de Hello utilizados en este comando son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f29af-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="f29af-117">**-u** -Hola nombre de usuario y una contraseña usan tooauthenticate solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="f29af-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="f29af-118">**-G**: indica que esta es una solicitud de operación GET.</span><span class="sxs-lookup"><span data-stu-id="f29af-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="f29af-119">Hola a partir de la dirección URL de hello, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, Hola iguales para todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="f29af-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="f29af-120">ruta de acceso de Hello, **/Status**, indica esa solicitud hello es tooreturn un estado de WebHCat (también conocido como Templeton) para servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="f29af-121">También puede solicitar versión Hola del subárbol mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f29af-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="f29af-122">Esta solicitud devuelve un toohello similar de respuesta siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="f29af-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="f29af-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="f29af-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="f29af-124">Hola de uso después de una tabla denominada toocreate **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="f29af-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="f29af-125">Hola después de parámetros que se utilizan con esta solicitud:</span><span class="sxs-lookup"><span data-stu-id="f29af-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="f29af-126">**-d** : desde `-G` no se utiliza, solicitud de hello tiene como valor predeterminado el método POST de toohello.</span><span class="sxs-lookup"><span data-stu-id="f29af-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="f29af-127">`-d`Especifica los valores de datos de Hola que se envían con la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="f29af-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="f29af-128">**User.nombre** -usuario Hola que se ejecuta el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="f29af-129">**ejecutar** -Hola tooexecute de instrucciones de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="f29af-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="f29af-130">**statusdir** -se escribió en el directorio de Hola que Hola estado para este trabajo.</span><span class="sxs-lookup"><span data-stu-id="f29af-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="f29af-131">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f29af-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="f29af-132">**DROP TABLE** -si ya existe una tabla de hello, se elimina.</span><span class="sxs-lookup"><span data-stu-id="f29af-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="f29af-133">**CREATE EXTERNAL TABLE** : crea una tabla "externa" nueva en Hive.</span><span class="sxs-lookup"><span data-stu-id="f29af-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="f29af-134">Tablas externas almacenan solo la definición de tabla hello en el subárbol.</span><span class="sxs-lookup"><span data-stu-id="f29af-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="f29af-135">Hola datos permanecen en la ubicación original de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f29af-136">Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo.</span><span class="sxs-lookup"><span data-stu-id="f29af-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="f29af-137">Por ejemplo, un proceso de carga de datos automatizado u otra operación de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f29af-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="f29af-138">Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="f29af-139">**FORMATO de fila** : cómo Hola datos tienen el formato.</span><span class="sxs-lookup"><span data-stu-id="f29af-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="f29af-140">los campos de Hello en cada registro están separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="f29af-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="f29af-141">**UBICACIÓN de archivo de texto de AS almacenados** : donde se almacenan los datos de hello (directorio de datos del ejemplo de Hola) y que se almacena como texto.</span><span class="sxs-lookup"><span data-stu-id="f29af-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="f29af-142">**Seleccione** -selecciona un recuento de todas las filas donde columna **t4** contiene el valor de hello **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="f29af-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="f29af-143">Esta instrucción devuelve un valor de **3** porque hay tres filas que contienen este valor.</span><span class="sxs-lookup"><span data-stu-id="f29af-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f29af-144">Tenga en cuenta que los espacios de hello entre las instrucciones de HiveQL se reemplazan por hello `+` caracteres cuando se usa con el doblez.</span><span class="sxs-lookup"><span data-stu-id="f29af-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="f29af-145">Los valores entre comillas que contengan un espacio, como delimitador de hello, no deben ser reemplazados por `+`.</span><span class="sxs-lookup"><span data-stu-id="f29af-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="f29af-146">**INPUT__FILE__NAME como '% 25.log'** : esta instrucción límites Hola búsqueda tooonly use archivos de. registro.</span><span class="sxs-lookup"><span data-stu-id="f29af-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f29af-147">Hola `%25` es la forma de codificación de dirección URL de Hola de %, por lo que es la condición real hello `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="f29af-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="f29af-148">Hola % tiene codificada, la dirección URL toobe tal y como se trata como un carácter especial en las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="f29af-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="f29af-149">Este comando debe devolver un Id. de trabajo que puede ser utilizados toocheck Hola estado del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="f29af-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="f29af-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="f29af-151">estado de hello toocheck de trabajo de hello, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f29af-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="f29af-152">Reemplace **JOBID** con valor Hola devuelta en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="f29af-153">Por ejemplo, si hello devolver valor era `{"id":"job_1415651640909_0026"}`, a continuación, **JOBID** sería `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="f29af-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="f29af-154">Si ha terminado el trabajo de hello, estado de hello es **correcto**.</span><span class="sxs-lookup"><span data-stu-id="f29af-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f29af-155">Esta solicitud Curl devuelve un documento de JavaScript Object Notation (JSON) con información sobre el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="f29af-156">Se utiliza Jq tooretrieve Hola solo el valor de estado.</span><span class="sxs-lookup"><span data-stu-id="f29af-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="f29af-157">Una vez que el estado de Hola de trabajo de hello ha cambiado demasiado**correcto**, se pueden recuperar resultados de Hola de trabajo de Hola desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f29af-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="f29af-158">Hola `statusdir` parámetro pasado con hello consulta contiene ubicación de Hola Hola del archivo de salida; en este caso, **/ejemplo/curl**.</span><span class="sxs-lookup"><span data-stu-id="f29af-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="f29af-159">Esta dirección almacena los resultados de Hola Hola **ejemplo/curl** directory Hola clústeres de almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f29af-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="f29af-160">Puede enumerar y descargar estos archivos mediante el uso de hello [CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f29af-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="f29af-161">Para obtener más información sobre el uso de hello CLI de Azure con el almacenamiento de Azure, vea hello [usar Azure CLI 2.0 con el almacenamiento de Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) documento.</span><span class="sxs-lookup"><span data-stu-id="f29af-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="f29af-162">Hola uso siguiendo las instrucciones toocreate una nueva tabla 'interna' denominada **registros de errores de**:</span><span class="sxs-lookup"><span data-stu-id="f29af-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="f29af-163">Estas instrucciones realizan Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f29af-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="f29af-164">**CREATE TABLE IF NOT EXISTS** : crea una tabla, si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="f29af-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="f29af-165">Esta instrucción crea una tabla interna, que se almacena en el almacén de datos de Hive de Hola y Hive administra completamente.</span><span class="sxs-lookup"><span data-stu-id="f29af-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f29af-166">A diferencia de las tablas externas, al quitar una tabla interna, eliminan datos subyacente de saludo.</span><span class="sxs-lookup"><span data-stu-id="f29af-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="f29af-167">**ALMACENA AS ORC** -almacena los datos de hello en formato optimizado fila columnas (ORC).</span><span class="sxs-lookup"><span data-stu-id="f29af-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="f29af-168">ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.</span><span class="sxs-lookup"><span data-stu-id="f29af-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="f29af-169">**INSERT OVERWRITE ... Seleccione** -selecciona las filas de hello **log4jLogs** tabla que contenga **[ERROR]**, a continuación, inserta Hola datos en hello **registros de errores de** tabla.</span><span class="sxs-lookup"><span data-stu-id="f29af-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="f29af-170">**Seleccione** -selecciona todas las filas de hello nueva **registros de errores de** tabla.</span><span class="sxs-lookup"><span data-stu-id="f29af-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="f29af-171">Usar Id. de trabajo de hello devolvió el estado de hello toocheck de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="f29af-172">Una vez que se ha realizado correctamente, utilice Hola CLI de Azure como se describió anteriormente toodownload y ver resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f29af-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="f29af-173">salida de Hello debe contener tres líneas, todas las cuales contienen **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="f29af-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="f29af-174"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f29af-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f29af-175">Si desea obtener información general sobre Hive con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f29af-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="f29af-176">Uso de Hive con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f29af-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="f29af-177">Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f29af-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f29af-178">Uso de Pig con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f29af-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f29af-179">Uso de MapReduce con Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="f29af-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f29af-180">Si usas Tez con Hive, vea Hola después de documentos para información de depuración:</span><span class="sxs-lookup"><span data-stu-id="f29af-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="f29af-181">Usar hello vista Ambari Tez en HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="f29af-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="f29af-182">Para obtener más información sobre Hola API de REST que se utiliza en este documento, vea hello [WebHCat referencia](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) documento.</span><span class="sxs-lookup"><span data-stu-id="f29af-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


