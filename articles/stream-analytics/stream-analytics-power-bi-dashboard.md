---
title: "panel de BI de aaaPower en análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Use un en tiempo real streaming Power BI panel toogather de business intelligence y análisis de datos de gran volumen de un trabajo de análisis de transmisiones."
keywords: "panel de análisis, panel en tiempo real"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="7f691-104">Stream Analytics y Power BI: panel de análisis en tiempo real de flujo de datos</span><span class="sxs-lookup"><span data-stu-id="7f691-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="7f691-105">Análisis de transmisiones de Azure le permite tootake aprovechar uno de hello iniciales herramientas de business intelligence, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="7f691-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="7f691-106">En este artículo, aprenderá a crear herramientas de inteligencia empresarial personalizadas utilizando Power BI como salida para los trabajos de Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7f691-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="7f691-107">También aprenderá cómo toocreate y usar un panel en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="7f691-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="7f691-108">Este artículo continúa a partir de análisis de transmisiones de hello [detección de fraudes en tiempo real](stream-analytics-real-time-fraud-detection.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7f691-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="7f691-109">Se basa en el flujo de trabajo de hello creado en este tutorial y agrega una Power BI, por lo que puede visualizar fraudulentas llamadas telefónicas que se detectó un trabajo de análisis de transmisión por secuencias de salida.</span><span class="sxs-lookup"><span data-stu-id="7f691-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="7f691-110">Puede ver un [vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que muestra este escenario.</span><span class="sxs-lookup"><span data-stu-id="7f691-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7f691-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7f691-111">Prerequisites</span></span>

<span data-ttu-id="7f691-112">Antes de empezar, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="7f691-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="7f691-113">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f691-113">An Azure account.</span></span>
* <span data-ttu-id="7f691-114">Una cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="7f691-114">An account for Power BI.</span></span> <span data-ttu-id="7f691-115">Puede usar una cuenta profesional o una cuenta educativa.</span><span class="sxs-lookup"><span data-stu-id="7f691-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="7f691-116">Una versión completada de hello [detección de fraudes en tiempo real](stream-analytics-real-time-fraud-detection.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7f691-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="7f691-117">tutorial de Hello incluye una aplicación que genera los metadatos de la llamada de teléfono ficticios.</span><span class="sxs-lookup"><span data-stu-id="7f691-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="7f691-118">En el tutorial de hello, crear un centro de eventos y enviar Hola concentrador de eventos de llamada de teléfono datos toohello de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="7f691-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="7f691-119">Escribir una consulta que detecta llamadas fraudulentas (llamadas de hello mismo número en hello mismo tiempo en distintas ubicaciones).</span><span class="sxs-lookup"><span data-stu-id="7f691-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="7f691-120">Incorporación del resultado de Power BI</span><span class="sxs-lookup"><span data-stu-id="7f691-120">Add Power BI output</span></span>
<span data-ttu-id="7f691-121">En el tutorial de detección de fraudes en tiempo real de hello, la salida de Hola se envía el almacenamiento de blobs de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7f691-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="7f691-122">En esta sección, agregará una salida que envía información tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="7f691-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="7f691-123">Hola portal de Azure, abra el trabajo de análisis de transmisión por secuencias de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7f691-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="7f691-124">Si ha usado el nombre sugerido de hello, el trabajo de Hola se denomina `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="7f691-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="7f691-125">Seleccione hello **salidas** cuadro en medio de Hola de panel de trabajo de hello y, a continuación, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="7f691-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="7f691-126">Como **Alias de salida**, escriba `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="7f691-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="7f691-127">Puede usar otro nombre.</span><span class="sxs-lookup"><span data-stu-id="7f691-127">You can use a different name.</span></span> <span data-ttu-id="7f691-128">Si lo hace, tome nota del mismo, porque necesita Hola nombre más adelante.</span><span class="sxs-lookup"><span data-stu-id="7f691-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="7f691-129">En **Receptor**, seleccione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="7f691-129">Under **Sink**, select **Power BI**.</span></span>

   ![Creación de una salida para Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="7f691-131">Haga clic en **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="7f691-131">Click **Authorize**.</span></span>

    <span data-ttu-id="7f691-132">Se abrirá una ventana donde puede especificar sus credenciales de Azure para una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="7f691-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Escriba las credenciales de acceso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="7f691-134">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="7f691-134">Enter your credentials.</span></span> <span data-ttu-id="7f691-135">Tenga en cuenta, a continuación, al escribir sus credenciales, está también da tooaccess de trabajo de análisis de transmisión por secuencias de permiso toohello su área de Power BI.</span><span class="sxs-lookup"><span data-stu-id="7f691-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="7f691-136">Cuando se le redirige toohello **nueva salida** hoja, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="7f691-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="7f691-137">**Área de trabajo de grupo**: seleccione un área de trabajo en el inquilino de Power BI donde desea que el conjunto de datos de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="7f691-138">**Nombre del conjunto de datos**: escriba `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="7f691-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="7f691-139">Puede usar otro nombre.</span><span class="sxs-lookup"><span data-stu-id="7f691-139">You can use a different name.</span></span> <span data-ttu-id="7f691-140">Si lo hace, apúntelo para recordarlo más tarde.</span><span class="sxs-lookup"><span data-stu-id="7f691-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="7f691-141">**Nombre de la tabla**: escriba `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="7f691-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="7f691-142">Actualmente, la salida de Power BI de trabajos de Stream Analytics solo puede tener una tabla en un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="7f691-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Área de trabajo de PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="7f691-144">Si Power BI tiene un conjunto de datos y tabla cuyas Hola mismos nombres que Hola que especifique en el trabajo de análisis de transmisiones de hello, Hola existentes se sobrescribe.</span><span class="sxs-lookup"><span data-stu-id="7f691-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="7f691-145">Se recomienda no crear explícitamente este conjunto de datos y la tabla en la cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="7f691-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="7f691-146">Se crean automáticamente al iniciar el trabajo de análisis de transmisiones y trabajo de Hola a partir del resultado bombeo Power BI.</span><span class="sxs-lookup"><span data-stu-id="7f691-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="7f691-147">Si la consulta de trabajo no devuelve ningún resultado, no se crean la tabla y conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="7f691-148">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7f691-148">Click **Create**.</span></span>

<span data-ttu-id="7f691-149">se crea el conjunto de datos de Hello con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="7f691-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="7f691-150">**defaultRetentionPolicy: BasicFIFO**: los datos tienen un orden FIFO, con un máximo de 200 000 filas.</span><span class="sxs-lookup"><span data-stu-id="7f691-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="7f691-151">**defaultMode: pushStreaming**: conjunto de datos de hello admite iconos de transmisión por secuencias y objetos visuales de informe basa tradicionales (conocido como)</span><span class="sxs-lookup"><span data-stu-id="7f691-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="7f691-152">inserción).</span><span class="sxs-lookup"><span data-stu-id="7f691-152">push).</span></span>

<span data-ttu-id="7f691-153">Actualmente, no se pueden crear conjuntos de datos con otras marcas.</span><span class="sxs-lookup"><span data-stu-id="7f691-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="7f691-154">Para obtener más información acerca de los conjuntos de datos de Power BI, consulte hello [API de REST de Power BI](https://msdn.microsoft.com/library/mt203562.aspx) referencia.</span><span class="sxs-lookup"><span data-stu-id="7f691-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="7f691-155">Escribir consulta Hola</span><span class="sxs-lookup"><span data-stu-id="7f691-155">Write hello query</span></span>

1. <span data-ttu-id="7f691-156">Hola cerrar **salidas** hoja y hoja de trabajo de toohello devuelto.</span><span class="sxs-lookup"><span data-stu-id="7f691-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="7f691-157">Haga clic en hello **consulta** cuadro.</span><span class="sxs-lookup"><span data-stu-id="7f691-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="7f691-158">Escriba Hola después de consulta.</span><span class="sxs-lookup"><span data-stu-id="7f691-158">Enter hello following query.</span></span> <span data-ttu-id="7f691-159">Esta consulta es similar toohello autocombinación que creó en el tutorial de detección de fraudes Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="7f691-160">Hello diferencia es que esta consulta envía resultados toohello nueva salida que ha creado (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="7f691-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="7f691-161">Si no asigna un nombre hello entrada `CallStream` en tutorial de detección de fraudes de hello, sustituya el nombre de `CallStream` en hello **FROM** y **UNIR** cláusulas de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="7f691-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7f691-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="7f691-163">Consulta de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="7f691-163">Test hello query</span></span>
<span data-ttu-id="7f691-164">Esta sección es opcional pero conveniente.</span><span class="sxs-lookup"><span data-stu-id="7f691-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="7f691-165">Si la aplicación de hello TelcoStreaming no se está ejecutando, inícielo siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7f691-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="7f691-166">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7f691-166">Open a command window.</span></span>
    * <span data-ttu-id="7f691-167">Carpeta de toohello vaya donde se telcogenerator.exe hello y archivos telcodatagen.exe.config modificado.</span><span class="sxs-lookup"><span data-stu-id="7f691-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="7f691-168">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7f691-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="7f691-169">Hola **consulta** hoja, haga clic en hello puntos siguiente toohello `CallStream` de entrada y, a continuación, seleccione **datos a partir de datos de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="7f691-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="7f691-170">Especifique que quiere datos correspondientes a tres minutos y haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f691-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="7f691-171">Espere hasta que se le notifica que se han tomado como muestra datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="7f691-172">Haga clic en **Probar** y asegúrese de que obtiene resultados.</span><span class="sxs-lookup"><span data-stu-id="7f691-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="7f691-173">Ejecutar trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="7f691-173">Run hello job</span></span>

1. <span data-ttu-id="7f691-174">Asegúrese de que está ejecutando la aplicación hello TelcoStreaming.</span><span class="sxs-lookup"><span data-stu-id="7f691-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="7f691-175">Hola cerrar **consulta** hoja.</span><span class="sxs-lookup"><span data-stu-id="7f691-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="7f691-176">En la hoja de trabajo de hello, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="7f691-176">In hello job blade, click **Start**.</span></span>

    ![Iniciar el trabajo de análisis de transmisiones de Hola](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="7f691-178">Su trabajo de análisis de transmisión por secuencias comienza buscando llamadas fraudulentas en secuencia de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="7f691-179">trabajo de Hello también crea el conjunto de datos de hello y una tabla en Power BI y comienza a enviar datos sobre Hola llamadas fraudulentas toothem.</span><span class="sxs-lookup"><span data-stu-id="7f691-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="7f691-180">Crear panel hello en Power BI</span><span class="sxs-lookup"><span data-stu-id="7f691-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="7f691-181">Vaya demasiado[Powerbi.com](https://powerbi.com) e inicie sesión con su cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="7f691-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="7f691-182">Si la consulta de trabajo de análisis de transmisiones de hello genera resultados, verá que ya se ha creado el conjunto de datos:</span><span class="sxs-lookup"><span data-stu-id="7f691-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Conjunto de datos de streaming en Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="7f691-184">En el área de trabajo, haga clic en **+&nbsp;Crear**.</span><span class="sxs-lookup"><span data-stu-id="7f691-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![botón Crear de Hello en el área de trabajo de Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="7f691-186">Cree otro panel y asígnele el nombre `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="7f691-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Creación de un panel y asignación de un nombre en el área de trabajo de Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="7f691-188">Hola parte superior de ventana hello, haga clic en **agregar icono**, seleccione **datos de transmisión personalizados**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7f691-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Conjunto de datos de streaming personalizados](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="7f691-190">En **YOUR DATSETS** (SUS CONJUNTOS DE DATOS), seleccione el conjunto de datos y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7f691-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Su conjunto de datos de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="7f691-192">En **tipo de visualización**, seleccione **tarjeta**y, a continuación, en hello **campos** lista, seleccione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="7f691-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Detalles de visualización del nuevo icono](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="7f691-194">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7f691-194">Click **Next**.</span></span>

8. <span data-ttu-id="7f691-195">Rellene detalles del icono, como el título y el subtítulo.</span><span class="sxs-lookup"><span data-stu-id="7f691-195">Fill in tile details like a title and subtitle.</span></span>

    ![Título y subtítulo del nuevo icono](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="7f691-197">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="7f691-197">Click **Apply**.</span></span>

    <span data-ttu-id="7f691-198">Ahora tiene un contador de fraudes.</span><span class="sxs-lookup"><span data-stu-id="7f691-198">Now you have a fraud counter!</span></span>

    ![Contador de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="7f691-200">Hola siga los pasos del nuevo tooadd un icono (comenzando con el paso 4).</span><span class="sxs-lookup"><span data-stu-id="7f691-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="7f691-201">En esta ocasión, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="7f691-201">This time, do hello following:</span></span>

    * <span data-ttu-id="7f691-202">Al obtener demasiado**tipo de visualización**, seleccione **gráfico de líneas**.</span><span class="sxs-lookup"><span data-stu-id="7f691-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="7f691-203">Agregue un eje y seleccione **windowend**.</span><span class="sxs-lookup"><span data-stu-id="7f691-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="7f691-204">Agregue un valor y seleccione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="7f691-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="7f691-205">Para **toodisplay de la ventana de tiempo**, seleccione Hola últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="7f691-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Creación de un icono de gráfico de líneas](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="7f691-207">Haga clic en **Siguiente**, agregue el título y el subtítulo y haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="7f691-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="7f691-208">panel de Power BI Hola le proporciona dos vistas de datos sobre las llamadas de fraudulentas según lo detecte en hello transmisión de datos.</span><span class="sxs-lookup"><span data-stu-id="7f691-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Panel de Power BI finalizado que muestra dos iconos de llamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="7f691-210">Más información sobre Power BI</span><span class="sxs-lookup"><span data-stu-id="7f691-210">Learn more about Power BI</span></span>

<span data-ttu-id="7f691-211">Este tutorial se muestra cómo toocreate solo unos tipos de visualizaciones para un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="7f691-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="7f691-212">Power BI puede ayudarle a crear otras herramientas de inteligencia empresarial de cliente para su organización.</span><span class="sxs-lookup"><span data-stu-id="7f691-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="7f691-213">Para obtener más ideas, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7f691-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="7f691-214">Para obtener otro ejemplo de un panel de Power BI, vea hello [Introducción a Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vídeo.</span><span class="sxs-lookup"><span data-stu-id="7f691-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="7f691-215">Para obtener más información acerca de cómo configurar el análisis de transmisión por secuencias de trabajo salida tooPower BI y uso de grupos de Power BI, revise hello [Power BI](stream-analytics-define-outputs.md#power-bi) sección de hello [análisis de transmisiones genera](stream-analytics-define-outputs.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="7f691-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="7f691-216">Para información sobre el uso en general de Power BI, vea [Paneles de Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="7f691-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="7f691-217">Más información sobre limitaciones y prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="7f691-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="7f691-218">Actualmente, se puede llamar a Power BI una vez por segundo aproximadamente.</span><span class="sxs-lookup"><span data-stu-id="7f691-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="7f691-219">Los objetos visuales de streaming admiten paquetes de 15 KB.</span><span class="sxs-lookup"><span data-stu-id="7f691-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="7f691-220">Más allá de eso, se producirá un error en la transmisión por secuencias de objetos visuales (pero inserción continúa toowork).</span><span class="sxs-lookup"><span data-stu-id="7f691-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="7f691-221">Debido a estas limitaciones, Power BI se presta de forma más natural toocases que el análisis de transmisiones de Azure lleva a una reducción de la carga de gran volumen de datos.</span><span class="sxs-lookup"><span data-stu-id="7f691-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="7f691-222">Se recomienda utilizar una ventana de saltos de tamaño constante o Hopping ventana tooensure que es de inserción de datos a lo sumo una inserción por segundo, y que llega a la consulta dentro de los requisitos de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="7f691-223">Hola siguiente ecuación toocompute Hola valor toogive puede usar la ventana en segundos:</span><span class="sxs-lookup"><span data-stu-id="7f691-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Ecuación 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="7f691-225">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7f691-225">For example:</span></span>

* <span data-ttu-id="7f691-226">Tiene 1000 dispositivos que envían datos a intervalos de un segundo.</span><span class="sxs-lookup"><span data-stu-id="7f691-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="7f691-227">Utilizas Hola SKU Pro de Power BI que admita 1.000.000 de filas por hora.</span><span class="sxs-lookup"><span data-stu-id="7f691-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="7f691-228">Desea toopublish Hola tamaño promedio de los datos por dispositivo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="7f691-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="7f691-229">Como resultado, se convierte en ecuación hello:</span><span class="sxs-lookup"><span data-stu-id="7f691-229">As a result, hello equation becomes:</span></span>

![Ecuación 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="7f691-231">Dada esta configuración, puede cambiar Hola original consulta toohello a continuación:</span><span class="sxs-lookup"><span data-stu-id="7f691-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="7f691-232">Renovar la autorización</span><span class="sxs-lookup"><span data-stu-id="7f691-232">Renew authorization</span></span>
<span data-ttu-id="7f691-233">Si la contraseña de hello cambió desde que se creó o autenticado por última vez el trabajo, debe tooreauthenticate su cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="7f691-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="7f691-234">Si la autenticación multifactor Azure está configurada en el inquilino de Azure Active Directory (Azure AD), también se necesita autorización de Power BI toorenew cada dos semanas.</span><span class="sxs-lookup"><span data-stu-id="7f691-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="7f691-235">Si no lo renueva, podría ver síntomas como la falta de salida del trabajo o un `Authenticate user error` en registros de operaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="7f691-236">Del mismo modo, si se inicia un trabajo después de hello token ha expirado, se produce un error y se produce un error en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="7f691-237">tooresolve este problema, detenga trabajo Hola que se ejecuta y vaya tooyour Power BI de salida.</span><span class="sxs-lookup"><span data-stu-id="7f691-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="7f691-238">tooavoid pérdida de datos, seleccione hello **renovar la autorización** vincular y, a continuación, reinicie el trabajo de hello **última hora de detención**.</span><span class="sxs-lookup"><span data-stu-id="7f691-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="7f691-239">Después de que se haya actualizado la autorización de hello con Power BI, aparecerá una alerta verde en hello autorización área tooreflect que se ha resuelto el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f691-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="7f691-240">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="7f691-240">Get help</span></span>
<span data-ttu-id="7f691-241">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="7f691-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f691-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f691-242">Next steps</span></span>
* [<span data-ttu-id="7f691-243">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7f691-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7f691-244">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7f691-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7f691-245">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="7f691-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7f691-246">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7f691-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7f691-247">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7f691-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
