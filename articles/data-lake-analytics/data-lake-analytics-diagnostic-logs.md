---
title: "registros de diagnóstico de aaaViewing de análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Comprender el funcionamiento toosetup y diagnóstico de acceso de los registros de datos de Azure análisis Lake "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="0f1a6-103">Acceso a los registros de diagnóstico de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0f1a6-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="0f1a6-104">Registro de diagnóstico le permite los seguimientos de auditoría de acceso de datos de toocollect.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="0f1a6-105">Estos registros proporcionan información como:</span><span class="sxs-lookup"><span data-stu-id="0f1a6-105">These logs provide information such as:</span></span>

* <span data-ttu-id="0f1a6-106">Una lista de usuarios que tiene acceso a datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="0f1a6-107">Con qué frecuencia se tiene acceso a datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="0f1a6-108">La cantidad de datos se almacena en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="0f1a6-109">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="0f1a6-109">Enable logging</span></span>

1. <span data-ttu-id="0f1a6-110">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f1a6-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0f1a6-111">Abra su cuenta de análisis de Data Lake y seleccione **registros de diagnóstico** de hello __Monitor__ sección.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="0f1a6-112">Después, seleccione __Activar diagnósticos__.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-112">Next, select __Turn on diagnostics__.</span></span>

    ![Activar la auditoría de toocollect de diagnóstico y registros de solicitudes](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="0f1a6-114">De __configuración de diagnóstico__, establezca too__On__ de estado de Hola y seleccionar opciones de registro.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="0f1a6-115">![Activar la auditoría de toocollect de diagnóstico y registros de solicitudes](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "habilitar registros de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="0f1a6-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="0f1a6-116">Establecer **estado** demasiado**en** tooenable el registro de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="0f1a6-117">Puede elegir datos hello toostore o proceso de tres maneras diferentes.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="0f1a6-118">Seleccione __tooa cuenta de almacenamiento de archivo__ toostore se registra en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="0f1a6-119">Utilice esta opción si desea que los datos de hello tooarchive.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="0f1a6-120">Si selecciona esta opción, debe proporcionar un almacenamiento de Azure cuenta toosave Hola los registros a.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="0f1a6-121">Seleccione **tooan concentrador de eventos de secuencia** tooan de datos de registro de toostream centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="0f1a6-122">Use esta opción si tiene una canalización de procesamiento de bajada que está analizando los registros entrantes en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="0f1a6-123">Si selecciona esta opción, debe proporcionar detalles de Hola para hello concentrador de eventos de Azure que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="0f1a6-124">Seleccione __enviar tooLog análisis__ toosend Hola datos toohello servicio de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="0f1a6-125">Utilice esta opción si desea toouse toogather de análisis de registros y analizar los registros.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="0f1a6-126">Especifique si desea que los registros de auditoría tooget, registros de solicitudes o ambos.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="0f1a6-127">Un registro de solicitudes captura todas las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-127">A request log captures every API request.</span></span> <span data-ttu-id="0f1a6-128">Un registro de auditoría registra todas las operaciones que esa solicitud de API desencadena.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="0f1a6-129">Para __tooa cuenta de almacenamiento de archivo__, especificar número de Hola de datos de hello tooretain días.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="0f1a6-130">Haga clic en __Guardar__.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0f1a6-131">Debe seleccionar __tooa cuenta de almacenamiento de archivo__, __tooan concentrador de eventos de secuencia__ o __enviar tooLog análisis__ antes de hacer clic hello __guardar__botón.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="0f1a6-132">Una vez que se ha habilitado la configuración de diagnóstico, puede devolver toohello __registros de diagnóstico__ hoja tooview Hola registros.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="0f1a6-133">Ver registros</span><span class="sxs-lookup"><span data-stu-id="0f1a6-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="0f1a6-134">Utilizar la vista de análisis de Data Lake Hola</span><span class="sxs-lookup"><span data-stu-id="0f1a6-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="0f1a6-135">En el análisis de Data Lake cuenta hoja, en **supervisión**, seleccione **registros de diagnóstico** y, a continuación, seleccione los registros para un toodisplay de entrada.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="0f1a6-136">![Ver registro de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Ver registros de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="0f1a6-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="0f1a6-137">Hello registros se dividen por categorías **los registros de auditoría** y **los registros de solicitudes**.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![entradas del registro](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="0f1a6-139">Registros de solicitudes de captura todas las solicitudes API realizadas en hello cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="0f1a6-140">Registros de auditoría son registros de toorequest similar pero proporciona un desglose de las operaciones de hello mucho más detallado.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="0f1a6-141">Por ejemplo, una llamada de API de carga única en un registro de solicitud podría producir varias operaciones "Append" en el registro de auditoría correspondiente.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="0f1a6-142">Haga clic en hello **descargar** vínculo para un toodownload de entrada de registro que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="0f1a6-143">Usar cuenta de almacenamiento de Azure de Hola que contiene datos del registro</span><span class="sxs-lookup"><span data-stu-id="0f1a6-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="0f1a6-144">Abra la hoja de cuenta de almacenamiento de Azure Hola asociado con análisis de Data Lake para el registro y, a continuación, haga clic en __Blobs__.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="0f1a6-145">Hola **servicio Blob** hoja muestra dos contenedores.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="0f1a6-146">![Ver registro de diagnóstico](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Ver registros de diagnóstico")</span><span class="sxs-lookup"><span data-stu-id="0f1a6-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="0f1a6-147">contenedor de Hello **auditoría de registros de visión** contiene registros de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="0f1a6-148">contenedor de Hello **las solicitudes de registros de visión** contiene registros de solicitudes de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="0f1a6-149">Dentro de estos contenedores, Hola registros se almacenan en hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="0f1a6-149">Within these containers, hello logs are stored under hello following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="0f1a6-150">Hola `##` las entradas de ruta de acceso de hello contengan Hola año, mes, día y hora en que Hola se creó el registro.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="0f1a6-151">Data Lake Analytics crea un archivo cada hora, por lo que `m=` siempre contiene un valor de `00`.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="0f1a6-152">Por ejemplo, podría ser el registro de auditoría de tooan de ruta de acceso completa de hello:</span><span class="sxs-lookup"><span data-stu-id="0f1a6-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="0f1a6-153">De igual forma, podría ser el registro de solicitudes de tooa de ruta de acceso completa de hello:</span><span class="sxs-lookup"><span data-stu-id="0f1a6-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="0f1a6-154">Estructura de los registros</span><span class="sxs-lookup"><span data-stu-id="0f1a6-154">Log structure</span></span>

<span data-ttu-id="0f1a6-155">Hello registros de auditoría y solicitud están en un formato estructurado de JSON.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="0f1a6-156">Request Logs</span><span class="sxs-lookup"><span data-stu-id="0f1a6-156">Request logs</span></span>

<span data-ttu-id="0f1a6-157">Este es un ejemplo de entrada en el registro de solicitudes con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="0f1a6-158">Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="0f1a6-159">Esquema de un registro de solicitud</span><span class="sxs-lookup"><span data-stu-id="0f1a6-159">Request log schema</span></span>

| <span data-ttu-id="0f1a6-160">Nombre</span><span class="sxs-lookup"><span data-stu-id="0f1a6-160">Name</span></span> | <span data-ttu-id="0f1a6-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f1a6-161">Type</span></span> | <span data-ttu-id="0f1a6-162">Description</span><span class="sxs-lookup"><span data-stu-id="0f1a6-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f1a6-163">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="0f1a6-163">time</span></span> |<span data-ttu-id="0f1a6-164">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-164">String</span></span> |<span data-ttu-id="0f1a6-165">Hola marca de tiempo (en UTC) del registro de hello</span><span class="sxs-lookup"><span data-stu-id="0f1a6-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="0f1a6-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="0f1a6-166">resourceId</span></span> |<span data-ttu-id="0f1a6-167">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-167">String</span></span> |<span data-ttu-id="0f1a6-168">identificador de Hello del recurso de Hola que realizó la operación de colocar en</span><span class="sxs-lookup"><span data-stu-id="0f1a6-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="0f1a6-169">categoría</span><span class="sxs-lookup"><span data-stu-id="0f1a6-169">category</span></span> |<span data-ttu-id="0f1a6-170">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-170">String</span></span> |<span data-ttu-id="0f1a6-171">categoría de registro de Hello.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-171">hello log category.</span></span> <span data-ttu-id="0f1a6-172">Por ejemplo, **Requests**.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="0f1a6-173">operationName</span><span class="sxs-lookup"><span data-stu-id="0f1a6-173">operationName</span></span> |<span data-ttu-id="0f1a6-174">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-174">String</span></span> |<span data-ttu-id="0f1a6-175">Nombre de operación de Hola que inició sesión.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="0f1a6-176">Por ejemplo, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="0f1a6-177">resultType</span><span class="sxs-lookup"><span data-stu-id="0f1a6-177">resultType</span></span> |<span data-ttu-id="0f1a6-178">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-178">String</span></span> |<span data-ttu-id="0f1a6-179">estado de Hola de operación de hello, por ejemplo, 200.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="0f1a6-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="0f1a6-180">callerIpAddress</span></span> |<span data-ttu-id="0f1a6-181">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-181">String</span></span> |<span data-ttu-id="0f1a6-182">dirección IP de Hola de cliente de Hola que realiza la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="0f1a6-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="0f1a6-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="0f1a6-183">correlationId</span></span> |<span data-ttu-id="0f1a6-184">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-184">String</span></span> |<span data-ttu-id="0f1a6-185">identificador de Hello del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-185">hello identifier of hello log.</span></span> <span data-ttu-id="0f1a6-186">Este valor puede ser toogroup usa un conjunto de entradas de registro relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="0f1a6-187">identidad</span><span class="sxs-lookup"><span data-stu-id="0f1a6-187">identity</span></span> |<span data-ttu-id="0f1a6-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="0f1a6-188">Object</span></span> |<span data-ttu-id="0f1a6-189">identidad de Hola que generó el registro de hello</span><span class="sxs-lookup"><span data-stu-id="0f1a6-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="0f1a6-190">propiedades</span><span class="sxs-lookup"><span data-stu-id="0f1a6-190">properties</span></span> |<span data-ttu-id="0f1a6-191">JSON</span><span class="sxs-lookup"><span data-stu-id="0f1a6-191">JSON</span></span> |<span data-ttu-id="0f1a6-192">Consulte la sección siguiente hello (esquema de propiedades de registro de solicitud) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="0f1a6-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="0f1a6-193">Esquema de propiedades de un registro de solicitud</span><span class="sxs-lookup"><span data-stu-id="0f1a6-193">Request log properties schema</span></span>

| <span data-ttu-id="0f1a6-194">Nombre</span><span class="sxs-lookup"><span data-stu-id="0f1a6-194">Name</span></span> | <span data-ttu-id="0f1a6-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f1a6-195">Type</span></span> | <span data-ttu-id="0f1a6-196">Description</span><span class="sxs-lookup"><span data-stu-id="0f1a6-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f1a6-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="0f1a6-197">HttpMethod</span></span> |<span data-ttu-id="0f1a6-198">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-198">String</span></span> |<span data-ttu-id="0f1a6-199">Hello método HTTP utilizado para la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="0f1a6-200">Por ejemplo, GET.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-200">For example, GET.</span></span> |
| <span data-ttu-id="0f1a6-201">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="0f1a6-201">Path</span></span> |<span data-ttu-id="0f1a6-202">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-202">String</span></span> |<span data-ttu-id="0f1a6-203">se realizó la operación de Hola de ruta de acceso de Hello en</span><span class="sxs-lookup"><span data-stu-id="0f1a6-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="0f1a6-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="0f1a6-204">RequestContentLength</span></span> |<span data-ttu-id="0f1a6-205">int</span><span class="sxs-lookup"><span data-stu-id="0f1a6-205">int</span></span> |<span data-ttu-id="0f1a6-206">longitud del contenido Hola de solicitud de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="0f1a6-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="0f1a6-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="0f1a6-207">ClientRequestId</span></span> |<span data-ttu-id="0f1a6-208">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-208">String</span></span> |<span data-ttu-id="0f1a6-209">Hola identificador que identifica de forma única esta solicitud</span><span class="sxs-lookup"><span data-stu-id="0f1a6-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="0f1a6-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="0f1a6-210">StartTime</span></span> |<span data-ttu-id="0f1a6-211">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-211">String</span></span> |<span data-ttu-id="0f1a6-212">hora de Hello en qué servidor recibido una petición Hola Hola</span><span class="sxs-lookup"><span data-stu-id="0f1a6-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="0f1a6-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="0f1a6-213">EndTime</span></span> |<span data-ttu-id="0f1a6-214">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-214">String</span></span> |<span data-ttu-id="0f1a6-215">tiempo de Hello en qué Hola servidor envió una respuesta</span><span class="sxs-lookup"><span data-stu-id="0f1a6-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="0f1a6-216">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="0f1a6-216">Audit logs</span></span>

<span data-ttu-id="0f1a6-217">Este es un ejemplo de entrada en el registro de auditoría con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="0f1a6-218">Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="0f1a6-219">Esquema de un registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="0f1a6-219">Audit log schema</span></span>

| <span data-ttu-id="0f1a6-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="0f1a6-220">Name</span></span> | <span data-ttu-id="0f1a6-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f1a6-221">Type</span></span> | <span data-ttu-id="0f1a6-222">Description</span><span class="sxs-lookup"><span data-stu-id="0f1a6-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f1a6-223">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="0f1a6-223">time</span></span> |<span data-ttu-id="0f1a6-224">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-224">String</span></span> |<span data-ttu-id="0f1a6-225">Hola marca de tiempo (en UTC) del registro de hello</span><span class="sxs-lookup"><span data-stu-id="0f1a6-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="0f1a6-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="0f1a6-226">resourceId</span></span> |<span data-ttu-id="0f1a6-227">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-227">String</span></span> |<span data-ttu-id="0f1a6-228">identificador de Hello del recurso de Hola que realizó la operación de colocar en</span><span class="sxs-lookup"><span data-stu-id="0f1a6-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="0f1a6-229">categoría</span><span class="sxs-lookup"><span data-stu-id="0f1a6-229">category</span></span> |<span data-ttu-id="0f1a6-230">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-230">String</span></span> |<span data-ttu-id="0f1a6-231">categoría de registro de Hello.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-231">hello log category.</span></span> <span data-ttu-id="0f1a6-232">Por ejemplo, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="0f1a6-233">operationName</span><span class="sxs-lookup"><span data-stu-id="0f1a6-233">operationName</span></span> |<span data-ttu-id="0f1a6-234">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-234">String</span></span> |<span data-ttu-id="0f1a6-235">Nombre de operación de Hola que inició sesión.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="0f1a6-236">Por ejemplo, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="0f1a6-237">resultType</span><span class="sxs-lookup"><span data-stu-id="0f1a6-237">resultType</span></span> |<span data-ttu-id="0f1a6-238">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-238">String</span></span> |<span data-ttu-id="0f1a6-239">Un subestado del estado del trabajo hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="0f1a6-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="0f1a6-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="0f1a6-240">resultSignature</span></span> |<span data-ttu-id="0f1a6-241">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-241">String</span></span> |<span data-ttu-id="0f1a6-242">Obtener más detalles sobre el estado del trabajo de hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="0f1a6-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="0f1a6-243">identidad</span><span class="sxs-lookup"><span data-stu-id="0f1a6-243">identity</span></span> |<span data-ttu-id="0f1a6-244">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-244">String</span></span> |<span data-ttu-id="0f1a6-245">usuario de Hola que solicitó la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-245">hello user that requested hello operation.</span></span> <span data-ttu-id="0f1a6-246">Por ejemplo: susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="0f1a6-247">propiedades</span><span class="sxs-lookup"><span data-stu-id="0f1a6-247">properties</span></span> |<span data-ttu-id="0f1a6-248">JSON</span><span class="sxs-lookup"><span data-stu-id="0f1a6-248">JSON</span></span> |<span data-ttu-id="0f1a6-249">Consulte la sección siguiente hello (esquema de propiedades de registro de auditoría) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="0f1a6-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="0f1a6-250">**resultType** y **resultSignature** proporcionan información sobre el resultado de hello de una operación y solo contiene un valor si se ha completado una operación.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="0f1a6-251">Por ejemplo, solo contienen un valor cuando **operationName** contiene un valor de **JobStarted** o **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="0f1a6-252">Esquema de propiedades de un registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="0f1a6-252">Audit log properties schema</span></span>

| <span data-ttu-id="0f1a6-253">Nombre</span><span class="sxs-lookup"><span data-stu-id="0f1a6-253">Name</span></span> | <span data-ttu-id="0f1a6-254">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f1a6-254">Type</span></span> | <span data-ttu-id="0f1a6-255">Description</span><span class="sxs-lookup"><span data-stu-id="0f1a6-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f1a6-256">JobId</span><span class="sxs-lookup"><span data-stu-id="0f1a6-256">JobId</span></span> |<span data-ttu-id="0f1a6-257">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-257">String</span></span> |<span data-ttu-id="0f1a6-258">trabajo de Hello Id. asignado toohello</span><span class="sxs-lookup"><span data-stu-id="0f1a6-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="0f1a6-259">JobName</span><span class="sxs-lookup"><span data-stu-id="0f1a6-259">JobName</span></span> |<span data-ttu-id="0f1a6-260">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-260">String</span></span> |<span data-ttu-id="0f1a6-261">nombre de Hola que se especificó para el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="0f1a6-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="0f1a6-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="0f1a6-262">JobRunTime</span></span> |<span data-ttu-id="0f1a6-263">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-263">String</span></span> |<span data-ttu-id="0f1a6-264">en tiempo de ejecución de Hello usa trabajos de hello tooprocess</span><span class="sxs-lookup"><span data-stu-id="0f1a6-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="0f1a6-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="0f1a6-265">SubmitTime</span></span> |<span data-ttu-id="0f1a6-266">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-266">String</span></span> |<span data-ttu-id="0f1a6-267">tiempo de presentación (en UTC) que el trabajo de hello envió</span><span class="sxs-lookup"><span data-stu-id="0f1a6-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="0f1a6-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="0f1a6-268">StartTime</span></span> |<span data-ttu-id="0f1a6-269">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-269">String</span></span> |<span data-ttu-id="0f1a6-270">trabajo Hola Hola empezó a ejecutarse después del envío (en UTC)</span><span class="sxs-lookup"><span data-stu-id="0f1a6-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="0f1a6-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="0f1a6-271">EndTime</span></span> |<span data-ttu-id="0f1a6-272">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-272">String</span></span> |<span data-ttu-id="0f1a6-273">finalizó el trabajo Hola Hola</span><span class="sxs-lookup"><span data-stu-id="0f1a6-273">hello time hello job ended</span></span> |
| <span data-ttu-id="0f1a6-274">Paralelismo</span><span class="sxs-lookup"><span data-stu-id="0f1a6-274">Parallelism</span></span> |<span data-ttu-id="0f1a6-275">String</span><span class="sxs-lookup"><span data-stu-id="0f1a6-275">String</span></span> |<span data-ttu-id="0f1a6-276">número de Hola de unidades de análisis de Data Lake solicitadas para este trabajo durante el envío</span><span class="sxs-lookup"><span data-stu-id="0f1a6-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="0f1a6-277">**SubmitTime**, **StartTime**, **EndTime** y **Parallelism** proporcionan información sobre una operación.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="0f1a6-278">Estas entradas solo contienen un valor si la operación se ha iniciado o completado.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="0f1a6-279">Por ejemplo, **SubmitTime** sólo contiene un valor una vez **operationName** tiene el valor de hello **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="0f1a6-280">Datos del registro de hello procesos</span><span class="sxs-lookup"><span data-stu-id="0f1a6-280">Process hello log data</span></span>

<span data-ttu-id="0f1a6-281">Análisis de Azure Data Lake proporciona un ejemplo sobre cómo tooprocess y analizar los datos de registro de saludo.</span><span class="sxs-lookup"><span data-stu-id="0f1a6-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="0f1a6-282">Puede encontrar el ejemplo hello en [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="0f1a6-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f1a6-283">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f1a6-283">Next steps</span></span>
* [<span data-ttu-id="0f1a6-284">Información general de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0f1a6-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
