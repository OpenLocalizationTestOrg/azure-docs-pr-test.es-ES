---
title: Panel de Power BI en Azure Stream Analytics | Microsoft Docs
description: "Utilice un panel de Power BI de streaming en tiempo real para reunir información de inteligencia empresarial y analizar grandes volúmenes de datos procedentes de un trabajo de Análisis de transmisiones."
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
ms.openlocfilehash: 874d9b8701a24deb3cc21aa74cb51870155c7c9c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="91777-104">Stream Analytics y Power BI: panel de análisis en tiempo real de flujo de datos</span><span class="sxs-lookup"><span data-stu-id="91777-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="91777-105">Azure Stream Analytics permite aprovechar una de las principales herramientas de inteligencia empresarial, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="91777-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="91777-106">En este artículo, aprenderá a crear herramientas de inteligencia empresarial personalizadas utilizando Power BI como salida para los trabajos de Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="91777-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="91777-107">También aprenderá a crear y usar un panel en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="91777-107">You also learn how to create and use a real-time dashboard.</span></span>

<span data-ttu-id="91777-108">Este artículo continúa a partir del tutorial [Detección de fraudes en tiempo real](stream-analytics-real-time-fraud-detection.md) de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="91777-108">This article continues from the Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="91777-109">Se basa en el flujo de trabajo creado en ese tutorial y agrega una salida de Power BI para que se puedan visualizar llamadas telefónicas fraudulentas detectadas por un trabajo de Streaming Analytics.</span><span class="sxs-lookup"><span data-stu-id="91777-109">It builds on the workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="91777-110">Puede ver un [vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que muestra este escenario.</span><span class="sxs-lookup"><span data-stu-id="91777-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="91777-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="91777-111">Prerequisites</span></span>

<span data-ttu-id="91777-112">Antes de empezar, asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="91777-112">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="91777-113">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="91777-113">An Azure account.</span></span>
* <span data-ttu-id="91777-114">Una cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-114">An account for Power BI.</span></span> <span data-ttu-id="91777-115">Puede usar una cuenta profesional o una cuenta educativa.</span><span class="sxs-lookup"><span data-stu-id="91777-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="91777-116">Versión completa del tutorial [Detección de fraudes en tiempo real](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="91777-116">A completed version of the [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="91777-117">El tutorial incluye una aplicación que genera metadatos de llamada telefónica ficticia.</span><span class="sxs-lookup"><span data-stu-id="91777-117">The tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="91777-118">En el tutorial, se crea un centro de eventos y se envían los datos de llamada telefónica de streaming al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="91777-118">In the tutorial, you create an event hub and send the streaming phone call data to the event hub.</span></span> <span data-ttu-id="91777-119">Escriba una consulta que detecte llamadas fraudulentas (llamadas del mismo número a la vez en distintas ubicaciones).</span><span class="sxs-lookup"><span data-stu-id="91777-119">You write a query that detects fraudulent calls (calls from the same number at the same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="91777-120">Incorporación del resultado de Power BI</span><span class="sxs-lookup"><span data-stu-id="91777-120">Add Power BI output</span></span>
<span data-ttu-id="91777-121">En el tutorial de detección de fraudes en tiempo real, la salida se envía a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="91777-121">In the real-time fraud detection tutorial, the output is sent to Azure Blob storage.</span></span> <span data-ttu-id="91777-122">En esta sección se agrega una salida que envía información a Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-122">In this section, you add an output that sends information to Power BI.</span></span>

1. <span data-ttu-id="91777-123">En Azure Portal, abra la cuenta de Stream Analytics que creó antes.</span><span class="sxs-lookup"><span data-stu-id="91777-123">In the Azure portal, open the Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="91777-124">Si usó el nombre sugerido, el trabajo se llama `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="91777-124">If you used the suggested name, the job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="91777-125">Active la casilla **Salidas** en el centro del panel de trabajo y seleccione **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="91777-125">Select the **Outputs** box in the middle of the job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="91777-126">Como **Alias de salida**, escriba `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="91777-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="91777-127">Puede usar otro nombre.</span><span class="sxs-lookup"><span data-stu-id="91777-127">You can use a different name.</span></span> <span data-ttu-id="91777-128">Si lo hace, tome nota del mismo, porque más adelante se necesita el nombre.</span><span class="sxs-lookup"><span data-stu-id="91777-128">If you do, make a note of it, because you need the name later.</span></span> 

4. <span data-ttu-id="91777-129">En **Receptor**, seleccione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="91777-129">Under **Sink**, select **Power BI**.</span></span>

   ![Creación de una salida para Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="91777-131">Haga clic en **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="91777-131">Click **Authorize**.</span></span>

    <span data-ttu-id="91777-132">Se abrirá una ventana donde puede especificar sus credenciales de Azure para una cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="91777-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Especificación de credenciales de acceso a Power BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="91777-134">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="91777-134">Enter your credentials.</span></span> <span data-ttu-id="91777-135">Luego, cuando escriba sus credenciales, tenga en cuenta que también le da permiso al trabajo de Stream Analytics para acceder a su área de Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-135">Be aware then when you enter your credentials, you're also giving permission to the Streaming Analytics job to access your Power BI area.</span></span>

7. <span data-ttu-id="91777-136">Cuando vuelva a la hoja **Nueva salida**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="91777-136">When you're returned to the **New output** blade, enter the following information:</span></span>

    * <span data-ttu-id="91777-137">**Área de trabajo de grupo**: seleccione el área de trabajo en el inquilino de Power BI en donde quiere crear el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="91777-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want to create the dataset.</span></span>
    * <span data-ttu-id="91777-138">**Nombre del conjunto de datos**: escriba `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="91777-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="91777-139">Puede usar otro nombre.</span><span class="sxs-lookup"><span data-stu-id="91777-139">You can use a different name.</span></span> <span data-ttu-id="91777-140">Si lo hace, apúntelo para recordarlo más tarde.</span><span class="sxs-lookup"><span data-stu-id="91777-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="91777-141">**Nombre de la tabla**: escriba `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="91777-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="91777-142">Actualmente, la salida de Power BI de trabajos de Stream Analytics solo puede tener una tabla en un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="91777-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Área de trabajo de PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="91777-144">Si Power BI tiene un conjunto de datos y una tabla con los mismos nombres que especifica en el trabajo de Stream Analytics, se sobrescribirán los existentes.</span><span class="sxs-lookup"><span data-stu-id="91777-144">If Power BI has a dataset and table that have the same names as the ones that you specify in the Stream Analytics job, the existing ones are overwritten.</span></span>
    > <span data-ttu-id="91777-145">Se recomienda no crear explícitamente este conjunto de datos y la tabla en la cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="91777-146">Se crearán automáticamente cuando inicie el trabajo de Stream Analytics y este empiece a enviar salida a Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-146">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span></span> <span data-ttu-id="91777-147">Si la consulta de trabajo no genera ningún resultado, el conjunto de datos y la tabla no se crean.</span><span class="sxs-lookup"><span data-stu-id="91777-147">If your job query doesn't return any results, the dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="91777-148">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="91777-148">Click **Create**.</span></span>

<span data-ttu-id="91777-149">El conjunto de datos se crea con la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="91777-149">The dataset is created with the following settings:</span></span>

* <span data-ttu-id="91777-150">**defaultRetentionPolicy: BasicFIFO**: los datos tienen un orden FIFO, con un máximo de 200 000 filas.</span><span class="sxs-lookup"><span data-stu-id="91777-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="91777-151">**defaultMode: pushStreaming**: el conjunto de datos admite iconos de streaming y objetos visuales tradicionales basados en informes (esto también se denomina inserción).</span><span class="sxs-lookup"><span data-stu-id="91777-151">**defaultMode: pushStreaming**: The dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="91777-152">inserción).</span><span class="sxs-lookup"><span data-stu-id="91777-152">push).</span></span>

<span data-ttu-id="91777-153">Actualmente, no se pueden crear conjuntos de datos con otras marcas.</span><span class="sxs-lookup"><span data-stu-id="91777-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="91777-154">Para más información sobre conjuntos de datos de Power BI, consulte la referencia de la [API de REST de Power BI](https://msdn.microsoft.com/library/mt203562.aspx).</span><span class="sxs-lookup"><span data-stu-id="91777-154">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-the-query"></a><span data-ttu-id="91777-155">Escritura de la consulta</span><span class="sxs-lookup"><span data-stu-id="91777-155">Write the query</span></span>

1. <span data-ttu-id="91777-156">Cierre la hoja **Salidas** y vuelva a la hoja del trabajo.</span><span class="sxs-lookup"><span data-stu-id="91777-156">Close the **Outputs** blade and return to the job blade.</span></span>

2. <span data-ttu-id="91777-157">Haga clic en el cuadro **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="91777-157">Click the **Query** box.</span></span> 

3. <span data-ttu-id="91777-158">Escriba la siguiente consulta.</span><span class="sxs-lookup"><span data-stu-id="91777-158">Enter the following query.</span></span> <span data-ttu-id="91777-159">Esta consulta es similar a la consulta de autocombinación que creó en el tutorial de detección de fraudes.</span><span class="sxs-lookup"><span data-stu-id="91777-159">This query is similar to the self-join query you created in the fraud-detection tutorial.</span></span> <span data-ttu-id="91777-160">La diferencia es que esta consulta envía los resultados a la nueva salida generada (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="91777-160">The difference is that this query sends results to the new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="91777-161">Si no asignó el nombre `CallStream` a la entrada en el tutorial de detección de fraudes, sustituya el nombre por `CallStream` en las cláusulas **FROM** y **JOIN** de la consulta.</span><span class="sxs-lookup"><span data-stu-id="91777-161">If you did not name the input `CallStream` in the fraud-detection tutorial, substitute your name for `CallStream` in the **FROM** and **JOIN** clauses in the query.</span></span>

        /* Our criteria for fraud:
        Calls made from the same caller to two phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where the caller is the same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where the switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="91777-162">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="91777-162">Click **Save**.</span></span>


## <a name="test-the-query"></a><span data-ttu-id="91777-163">Prueba de la consulta</span><span class="sxs-lookup"><span data-stu-id="91777-163">Test the query</span></span>
<span data-ttu-id="91777-164">Esta sección es opcional pero conveniente.</span><span class="sxs-lookup"><span data-stu-id="91777-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="91777-165">Si la aplicación TelcoStreaming no se ejecuta en este momento, siga estos pasos para iniciarla:</span><span class="sxs-lookup"><span data-stu-id="91777-165">If the TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="91777-166">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="91777-166">Open a command window.</span></span>
    * <span data-ttu-id="91777-167">Vaya a la carpeta donde se encuentran los archivos telcogenerator.exe y telcodatagen.exe.config modificado.</span><span class="sxs-lookup"><span data-stu-id="91777-167">Go to the folder where the telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="91777-168">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="91777-168">Run the following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="91777-169">En la hoja **Consulta**, haga clic en los puntos que aparecen junto a la entrada `CallStream` y seleccione **Datos de ejemplo de la entrada**.</span><span class="sxs-lookup"><span data-stu-id="91777-169">In the **Query** blade, click the dots next to the `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="91777-170">Especifique que quiere datos correspondientes a tres minutos y haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="91777-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="91777-171">Espere a que se le notifique que se ha realizado un muestreo de los datos.</span><span class="sxs-lookup"><span data-stu-id="91777-171">Wait until you're notified that the data has been sampled.</span></span>

4. <span data-ttu-id="91777-172">Haga clic en **Probar** y asegúrese de que obtiene resultados.</span><span class="sxs-lookup"><span data-stu-id="91777-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-the-job"></a><span data-ttu-id="91777-173">Ejecución del trabajo</span><span class="sxs-lookup"><span data-stu-id="91777-173">Run the job</span></span>

1. <span data-ttu-id="91777-174">Asegúrese de que la aplicación TelcoStreaming se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="91777-174">Make sure that the TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="91777-175">Cierre la hoja **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="91777-175">Close the **Query** blade.</span></span>

3. <span data-ttu-id="91777-176">En la hoja del trabajo, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="91777-176">In the job blade, click **Start**.</span></span>

    ![Inicio del trabajo de Análisis de transmisiones](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="91777-178">El trabajo de Stream Analytics empieza a buscar llamadas fraudulentas en el flujo entrante.</span><span class="sxs-lookup"><span data-stu-id="91777-178">Your Streaming Analytics job starts looking for fraudulent calls in the incoming stream.</span></span> <span data-ttu-id="91777-179">También crea el conjunto de datos y la tabla en Power BI y empieza a enviarles datos sobre las llamadas fraudulentas.</span><span class="sxs-lookup"><span data-stu-id="91777-179">The job also creates the dataset and table in Power BI and starts sending data about the fraudulent calls to them.</span></span>


## <a name="create-the-dashboard-in-power-bi"></a><span data-ttu-id="91777-180">Creación del panel en Power BI</span><span class="sxs-lookup"><span data-stu-id="91777-180">Create the dashboard in Power BI</span></span>

1. <span data-ttu-id="91777-181">Vaya a [Powerbi.com](https://powerbi.com) e inicie sesión con su cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="91777-181">Go to [Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="91777-182">Si la consulta del trabajo de Stream Analytics genera resultados, verá que el conjunto de datos ya se ha creado:</span><span class="sxs-lookup"><span data-stu-id="91777-182">If the Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Conjunto de datos de streaming en Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="91777-184">En el área de trabajo, haga clic en **+&nbsp;Crear**.</span><span class="sxs-lookup"><span data-stu-id="91777-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Botón Crear en el área de trabajo de Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="91777-186">Cree otro panel y asígnele el nombre `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="91777-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Creación de un panel y asignación de un nombre en el área de trabajo de Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="91777-188">En la parte superior de la ventana, haga clic en **Agregar icono**, seleccione **DATOS DE TRANSMISIÓN PERSONALIZADOS** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="91777-188">At the top of the window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Conjunto de datos de streaming personalizados](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="91777-190">En **YOUR DATSETS** (SUS CONJUNTOS DE DATOS), seleccione el conjunto de datos y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="91777-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Su conjunto de datos de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="91777-192">En **Tipo de visualización**, seleccione **Tarjeta** y luego, en la lista **Campos**, seleccione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="91777-192">Under **Visualization Type**, select **Card**, and then in the **Fields** list, select **fraudulentcalls**.</span></span>

    ![Detalles de visualización del nuevo icono](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="91777-194">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="91777-194">Click **Next**.</span></span>

8. <span data-ttu-id="91777-195">Rellene detalles del icono, como el título y el subtítulo.</span><span class="sxs-lookup"><span data-stu-id="91777-195">Fill in tile details like a title and subtitle.</span></span>

    ![Título y subtítulo del nuevo icono](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="91777-197">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="91777-197">Click **Apply**.</span></span>

    <span data-ttu-id="91777-198">Ahora tiene un contador de fraudes.</span><span class="sxs-lookup"><span data-stu-id="91777-198">Now you have a fraud counter!</span></span>

    ![Contador de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="91777-200">Siga de nuevo los pasos para agregar un icono (a partir del paso 4).</span><span class="sxs-lookup"><span data-stu-id="91777-200">Follow the steps again to add a tile (starting with step 4).</span></span> <span data-ttu-id="91777-201">Esta vez, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="91777-201">This time, do the following:</span></span>

    * <span data-ttu-id="91777-202">Cuando obtenga el **Tipo de visualización**, seleccione **Gráfico de líneas**.</span><span class="sxs-lookup"><span data-stu-id="91777-202">When you get to **Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="91777-203">Agregue un eje y seleccione **windowend**.</span><span class="sxs-lookup"><span data-stu-id="91777-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="91777-204">Agregue un valor y seleccione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="91777-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="91777-205">En **Período de tiempo para mostrar**, seleccione los últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="91777-205">For **Time window to display**, select the last 10 minutes.</span></span>

    ![Creación de un icono de gráfico de líneas](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="91777-207">Haga clic en **Siguiente**, agregue el título y el subtítulo y haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="91777-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="91777-208">El panel de Power BI le ofrece ahora dos vistas de datos sobre las llamadas fraudulentas detectadas en los datos de streaming.</span><span class="sxs-lookup"><span data-stu-id="91777-208">The Power BI dashboard now gives you two views of data about fraudulent calls as detected in the streaming data.</span></span>

    ![Panel de Power BI finalizado que muestra dos iconos de llamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="91777-210">Más información sobre Power BI</span><span class="sxs-lookup"><span data-stu-id="91777-210">Learn more about Power BI</span></span>

<span data-ttu-id="91777-211">Este tutorial solo muestra cómo crear algunos tipos de visualizaciones para un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="91777-211">This tutorial demonstrates how to create only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="91777-212">Power BI puede ayudarle a crear otras herramientas de inteligencia empresarial de cliente para su organización.</span><span class="sxs-lookup"><span data-stu-id="91777-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="91777-213">Para obtener otras ideas, vea los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="91777-213">For more ideas, see the following resources:</span></span>

* <span data-ttu-id="91777-214">Para obtener otro ejemplo de un panel de Power BI, vea el vídeo [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) .</span><span class="sxs-lookup"><span data-stu-id="91777-214">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="91777-215">Para más información sobre cómo configurar una salida de trabajo de Stream Analytics en Power BI y utilizar grupos de Power BI, revise la sección [Power BI](stream-analytics-define-outputs.md#power-bi) del artículo [Salidas de Stream Analytics](stream-analytics-define-outputs.md).</span><span class="sxs-lookup"><span data-stu-id="91777-215">For more information about configuring Streaming Analytics job output to Power BI and using Power BI groups, review the [Power BI](stream-analytics-define-outputs.md#power-bi) section of the [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="91777-216">Para información sobre el uso en general de Power BI, vea [Paneles de Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="91777-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="91777-217">Más información sobre limitaciones y prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="91777-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="91777-218">Actualmente, se puede llamar a Power BI una vez por segundo aproximadamente.</span><span class="sxs-lookup"><span data-stu-id="91777-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="91777-219">Los objetos visuales de streaming admiten paquetes de 15 KB.</span><span class="sxs-lookup"><span data-stu-id="91777-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="91777-220">Si el tamaño es superior, se producirá un error en los objetos visuales de streaming (pero la inserción continuará funcionando).</span><span class="sxs-lookup"><span data-stu-id="91777-220">Beyond that, streaming visuals fail (but push continues to work).</span></span> <span data-ttu-id="91777-221">Gracias a estas limitaciones, Power BI se presta de forma más natural a los casos en los que Azure Stream Analytics realiza una reducción considerable de la carga de datos.</span><span class="sxs-lookup"><span data-stu-id="91777-221">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="91777-222">Se recomienda utilizar una ventana de saltos de tamaño constante o una ventana de salto para asegurarse de que la inserción de datos es a lo sumo de una inserción por segundo y de que la consulta se ajusta a los requisitos de capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="91777-222">We recommend using a Tumbling window or Hopping window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span></span>

<span data-ttu-id="91777-223">Puede utilizar la siguiente ecuación para calcular el valor que asignar a la ventana en segundos:</span><span class="sxs-lookup"><span data-stu-id="91777-223">You can use the following equation to compute the value to give your window in seconds:</span></span>

![Ecuación 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="91777-225">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="91777-225">For example:</span></span>

* <span data-ttu-id="91777-226">Tiene 1000 dispositivos que envían datos a intervalos de un segundo.</span><span class="sxs-lookup"><span data-stu-id="91777-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="91777-227">Está usando Power BI Pro SKU que admite 1 000 000 de filas por hora.</span><span class="sxs-lookup"><span data-stu-id="91777-227">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="91777-228">Desea publicar la cantidad media de datos por dispositivo en Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-228">You want to publish the amount of average data per device to Power BI.</span></span>

<span data-ttu-id="91777-229">En consecuencia, la ecuación se convierte en:</span><span class="sxs-lookup"><span data-stu-id="91777-229">As a result, the equation becomes:</span></span>

![Ecuación 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="91777-231">Con esta configuración, se puede cambiar la consulta original a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="91777-231">Given this configuration, you can change the original query to the following:</span></span>

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


### <a name="renew-authorization"></a><span data-ttu-id="91777-232">Renovar la autorización</span><span class="sxs-lookup"><span data-stu-id="91777-232">Renew authorization</span></span>
<span data-ttu-id="91777-233">Si la contraseña ha cambiado desde que se creó o autenticó por última vez el trabajo, tendrá que volver a autenticar la cuenta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-233">If the password has changed since your job was created or last authenticated, you need to reauthenticate your Power BI account.</span></span> <span data-ttu-id="91777-234">Si Azure Multi-Factor Authentication se configura en el inquilino de Azure Active Directory (Azure AD), también debe renovar la autorización de Power BI cada dos semanas.</span><span class="sxs-lookup"><span data-stu-id="91777-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span></span> <span data-ttu-id="91777-235">Si no se renueva, podrían aparecer síntomas, como la ausencia de salida del trabajo o un `Authenticate user error` en los registros de operaciones.</span><span class="sxs-lookup"><span data-stu-id="91777-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in the operation logs.</span></span>

<span data-ttu-id="91777-236">De forma similar, si un trabajo intenta iniciarse después de que el token haya caducado, se producirá un error y no se iniciará.</span><span class="sxs-lookup"><span data-stu-id="91777-236">Similarly, if a job starts after the token has expired, an error occurs and the job fails.</span></span> <span data-ttu-id="91777-237">Para resolver este problema, detenga el trabajo en ejecución y vaya a la salida de Power BI.</span><span class="sxs-lookup"><span data-stu-id="91777-237">To resolve this issue, stop the job that's running and go to your Power BI output.</span></span> <span data-ttu-id="91777-238">A fin de evitar que se pierdan datos, seleccione el vínculo **Renovar autorización** y reinicie el trabajo desde la **Hora de la última detención**.</span><span class="sxs-lookup"><span data-stu-id="91777-238">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span></span>

<span data-ttu-id="91777-239">Después de que la autorización se haya actualizado con Power BI, se mostrará una alerta verde en el área de autorización para indicar que el problema se ha resuelto.</span><span class="sxs-lookup"><span data-stu-id="91777-239">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="91777-240">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="91777-240">Get help</span></span>
<span data-ttu-id="91777-241">Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="91777-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91777-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91777-242">Next steps</span></span>
* [<span data-ttu-id="91777-243">Introducción a Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="91777-243">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="91777-244">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="91777-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="91777-245">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="91777-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="91777-246">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="91777-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="91777-247">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="91777-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
