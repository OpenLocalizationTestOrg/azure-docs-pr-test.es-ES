---
title: "Integración de Azure Stream Analytics y Machine Learning | Microsoft Docs"
description: "Cómo utilizar una función definida por el usuario y Aprendizaje automático en un trabajo de Análisis de transmisiones"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: 023033d5479fcf0e2dff168b6604431eef283d3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="9a660-103">Análisis de opiniones mediante Azure Stream Analytics y Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9a660-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="9a660-104">En este artículo se explica cómo configurar rápidamente un trabajo sencillo de Azure Stream Analytics que integre Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9a660-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="9a660-105">Un modelo de análisis de opiniones de Machine Learning de la galería de Cortana Intelligence se usa para analizar datos de texto que se están transmitiendo y determinar la puntuación de opiniones en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="9a660-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span></span> <span data-ttu-id="9a660-106">Cortana Intelligence Suite permite realizar esta tarea sin preocuparse por las complejidades de la creación de un modelo de análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="9a660-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="9a660-107">Puede aplicar lo que aprenda en este artículo a escenarios como estos:</span><span class="sxs-lookup"><span data-stu-id="9a660-107">You can apply what you learn from this article to scenarios such as these:</span></span>

* <span data-ttu-id="9a660-108">Análisis de opiniones en tiempo real en datos de Twitter que se están transmitiendo.</span><span class="sxs-lookup"><span data-stu-id="9a660-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="9a660-109">Análisis de registros de chats de clientes con el personal de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="9a660-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="9a660-110">Evaluación de comentarios en foros, blogs y vídeos.</span><span class="sxs-lookup"><span data-stu-id="9a660-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="9a660-111">Muchos otros escenarios de puntuación predictiva en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="9a660-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="9a660-112">En un escenario real, los datos se obtendrían directamente de un flujo de datos de Twitter.</span><span class="sxs-lookup"><span data-stu-id="9a660-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span></span> <span data-ttu-id="9a660-113">Para simplificar el tutorial, se ha escrito de modo que el trabajo de Streaming Analytics obtenga los tweets de un archivo CSV de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9a660-113">To simplify the tutorial, we've written it so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="9a660-114">Puede crear su propio archivo CSV o usar un archivo CSV de ejemplo, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="9a660-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span></span>

![tweets de ejemplo de un archivo CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="9a660-116">El trabajo de Streaming Analytics que cree aplicará el modelo de análisis de opiniones como una función definida por el usuario (UDF) a los datos de texto de ejemplo del almacén de blobs.</span><span class="sxs-lookup"><span data-stu-id="9a660-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="9a660-117">La salida (el resultado del análisis de opiniones) se escribe en el mismo almacén de blobs en otro archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="9a660-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span></span> 

<span data-ttu-id="9a660-118">La imagen siguiente muestra esta configuración.</span><span class="sxs-lookup"><span data-stu-id="9a660-118">The following figure demonstrates this configuration.</span></span> <span data-ttu-id="9a660-119">Como se ha indicado, para un escenario más realista, puede sustituir el almacenamiento de blobs por datos de Twitter que se estén transmitiendo desde una entrada de Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="9a660-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="9a660-120">Además, puede crear una virtualización en tiempo real de [Microsoft Power BI](https://powerbi.microsoft.com/) de la opinión agregada.</span><span class="sxs-lookup"><span data-stu-id="9a660-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![Información general sobre la integración de Stream Analytics Machine Learning](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="9a660-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9a660-122">Prerequisites</span></span>
<span data-ttu-id="9a660-123">Antes de empezar, asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9a660-123">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="9a660-124">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="9a660-124">An active Azure subscription.</span></span>
* <span data-ttu-id="9a660-125">Un archivo CSV con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="9a660-125">A CSV file with some data in it.</span></span> <span data-ttu-id="9a660-126">Puede descargar el archivo mostrado anteriormente desde [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv) o bien puede crear su propio archivo.</span><span class="sxs-lookup"><span data-stu-id="9a660-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="9a660-127">En este artículo se da por hecho que está usando el archivo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a660-127">For this article, we assume that you're using the file from GitHub.</span></span>

<span data-ttu-id="9a660-128">En general, para realizar las tareas explicadas en este artículo, hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9a660-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span></span>

1. <span data-ttu-id="9a660-129">Crear una cuenta de Azure Storage y un contenedor de almacenamiento de blobs y cargar un archivo de entrada con formato CSV en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="9a660-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span></span>
3. <span data-ttu-id="9a660-130">Agregar un modelo de análisis de opiniones de la galería de Cortana Intelligence al área de trabajo de Azure Machine Learning e implementar este modelo como servicio web en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a660-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span></span>
5. <span data-ttu-id="9a660-131">Crear un trabajo de Stream Analytics que llame a este servicio web como una función para determinar la opinión sobre la entrada de texto.</span><span class="sxs-lookup"><span data-stu-id="9a660-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span></span>
6. <span data-ttu-id="9a660-132">Iniciar el trabajo de Stream Analytics y comprobar el resultado.</span><span class="sxs-lookup"><span data-stu-id="9a660-132">Start the Stream Analytics job and check the output.</span></span>

## <a name="create-a-storage-container-and-upload-the-csv-input-file"></a><span data-ttu-id="9a660-133">Creación de un contenedor de almacenamiento y carga del archivo de entrada CSV</span><span class="sxs-lookup"><span data-stu-id="9a660-133">Create a storage container and upload the CSV input file</span></span>
<span data-ttu-id="9a660-134">Para este paso puede usar cualquier archivo CSV, por ejemplo alguno de los disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a660-134">For this step, you can use any CSV file, such as the one available from GitHub.</span></span>

1. <span data-ttu-id="9a660-135">En Azure Portal, haga clic en **Nuevo** &gt; **Almacenamiento** &gt; **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="9a660-135">In the Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![creación de una nueva cuenta de almacenamiento](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="9a660-137">Proporcione un nombre (`samldemo` en el ejemplo).</span><span class="sxs-lookup"><span data-stu-id="9a660-137">Provide a name (`samldemo` in the example).</span></span> <span data-ttu-id="9a660-138">El nombre solo puede incluir letras minúsculas y números y debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="9a660-138">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="9a660-139">Especifique un grupo de recursos existente y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="9a660-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="9a660-140">Con respecto a la ubicación, se recomienda que todos los recursos creados en este tutorial usen la misma.</span><span class="sxs-lookup"><span data-stu-id="9a660-140">For location, we recommend that all the resources created in this tutorial use the same location.</span></span>

    ![especificación de los detalles de la cuenta de almacenamiento](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="9a660-142">En Azure Portal, seleccione la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9a660-142">In the Azure portal, select the storage account.</span></span> <span data-ttu-id="9a660-143">En la hoja de la cuenta de almacenamiento, haga clic en **Contenedores** y luego haga clic en **+&nbsp;Contenedor** para crear el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9a660-143">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span></span>

    ![creación de contenedor de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="9a660-145">Proporcione un nombre para el contenedor (`azuresamldemoblob` en el ejemplo) y compruebe que **Tipo de acceso** está establecido en **Blob**.</span><span class="sxs-lookup"><span data-stu-id="9a660-145">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span></span> <span data-ttu-id="9a660-146">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9a660-146">When you're done, click **OK**.</span></span>

    ![especificación de los detalles del contenedor de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="9a660-148">En la hoja **Contenedores**, seleccione el nuevo contenedor, con lo que se abre la hoja de ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="9a660-148">In the **Containers** blade, select the new container, which opens the blade for that container.</span></span>

7. <span data-ttu-id="9a660-149">Haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="9a660-149">Click **Upload**.</span></span>

    ![botón "Cargar" de un contenedor](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="9a660-151">En la hoja **Cargar blob**, especifique el archivo CSV que quiere usar para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a660-151">In the **Upload blob** blade, specify the CSV file that you want to use for this tutorial.</span></span> <span data-ttu-id="9a660-152">En **Tipo de blob**, seleccione **Blob en bloques** y establezca el tamaño de bloque en 4 MB, que es suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a660-152">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span></span>

    ![carga del archivo de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="9a660-154">Haga clic en el botón **Cargar** en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="9a660-154">Click the **Upload** button at the bottom of the blade.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="9a660-155">Adición del modelo de análisis de opinión desde la galería de Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="9a660-155">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>

<span data-ttu-id="9a660-156">Ahora que los datos de ejemplo están en un blob, puede habilitar el modelo de análisis de opiniones de la galería de Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="9a660-156">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="9a660-157">Vaya a la página de [modelo predictivo de análisis de opiniones](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) de la galería de Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="9a660-157">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="9a660-158">Haga clic en **Abrir en Studio**.</span><span class="sxs-lookup"><span data-stu-id="9a660-158">Click **Open in Studio**.</span></span>  
   
   ![Aprendizaje automático de Análisis de transmisiones, abrir Aprendizaje automático](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="9a660-160">Inicie sesión para dirigirse al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a660-160">Sign in to go to the workspace.</span></span> <span data-ttu-id="9a660-161">Seleccione una ubicación.</span><span class="sxs-lookup"><span data-stu-id="9a660-161">Select a location.</span></span>

4. <span data-ttu-id="9a660-162">Haga clic en **Ejecutar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="9a660-162">Click **Run** at the bottom of the page.</span></span> <span data-ttu-id="9a660-163">El proceso se ejecuta, lo que lleva aproximadamente un minuto.</span><span class="sxs-lookup"><span data-stu-id="9a660-163">The process runs, which takes about a minute.</span></span>

   ![ejecución del experimento en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="9a660-165">Una vez que el proceso se ha ejecutado correctamente, seleccione **Implementar servicio web** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="9a660-165">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span></span>

   ![implementación del experimento como un servicio web en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="9a660-167">Para comprobar que el modelo de análisis de opiniones está listo para su uso, haga clic en el botón **Probar**.</span><span class="sxs-lookup"><span data-stu-id="9a660-167">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span></span> <span data-ttu-id="9a660-168">Proporcione algún texto de entrada, como "Me encanta Microsoft".</span><span class="sxs-lookup"><span data-stu-id="9a660-168">Provide text input such as "I love Microsoft".</span></span> 

   ![prueba del experimento en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="9a660-170">Si la prueba funciona, verá un resultado similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9a660-170">If the test works, you see a result similar to the following example:</span></span>

   ![resultados de la prueba en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="9a660-172">En la columna **Aplicaciones**, haga clic en el vínculo de **libro de Excel 2010 o anterior** para descargar un libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="9a660-172">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span></span> <span data-ttu-id="9a660-173">El libro contiene una clave de API y la dirección URL que se necesitan más adelante para configurar el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9a660-173">The workbook contains the an API key and the URL that you need later to set up the Stream Analytics job.</span></span>

    ![Aprendizaje automático de Análisis de transmisiones, vista rápida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="9a660-175">Creación de un trabajo de Análisis de transmisiones que usa el modelo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="9a660-175">Create a Stream Analytics job that uses the Machine Learning model</span></span>

<span data-ttu-id="9a660-176">Ahora puede crear un trabajo de Stream Analytics que lea los tweets de ejemplo del archivo CSV de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9a660-176">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="9a660-177">Creación del trabajo</span><span class="sxs-lookup"><span data-stu-id="9a660-177">Create the job</span></span>

1. <span data-ttu-id="9a660-178">Vaya al [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a660-178">Go to the [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="9a660-179">Haga clic en **Nuevo** > **Internet de las cosas** > **Trabajo de Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="9a660-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![ruta de acceso del portal de Azure para acceder a un nuevo trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="9a660-181">Ponga el nombre `azure-sa-ml-demo` al trabajo, especifique una suscripción, especifique un grupo de recursos existente o cree uno nuevo y seleccione la ubicación del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a660-181">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span></span>

   ![especificación de la configuración del nuevo trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-the-job-input"></a><span data-ttu-id="9a660-183">Configuración de la entrada de trabajo</span><span class="sxs-lookup"><span data-stu-id="9a660-183">Configure the job input</span></span>
<span data-ttu-id="9a660-184">El trabajo obtiene su entrada del archivo CSV cargado anteriormente en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9a660-184">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span></span>

1. <span data-ttu-id="9a660-185">Una vez creado el trabajo, en la opción **Topología de trabajo** de la hoja del trabajo, haga clic en el cuadro **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="9a660-185">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** box.</span></span>  
   
   ![cuadro "Entradas" de la hoja del trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="9a660-187">En la hoja **Entradas**, haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9a660-187">In the **Inputs** blade, click **+ Add**.</span></span>

   ![botón "Agregar" para agregar una entrada al trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="9a660-189">Rellene la hoja **Nueva entrada** con estos valores:</span><span class="sxs-lookup"><span data-stu-id="9a660-189">Fill out the **New input** blade with these values:</span></span>

    * <span data-ttu-id="9a660-190">**Alias de entrada**: use el nombre `datainput`.</span><span class="sxs-lookup"><span data-stu-id="9a660-190">**Input alias**: Use the name `datainput`.</span></span>
    * <span data-ttu-id="9a660-191">**Tipo de origen**: seleccione **Flujo de datos**.</span><span class="sxs-lookup"><span data-stu-id="9a660-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="9a660-192">**Origen**: seleccione **Almacenamiento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="9a660-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="9a660-193">**Opción de importación**: seleccione **Usar almacenamiento de blobs de la suscripción actual**.</span><span class="sxs-lookup"><span data-stu-id="9a660-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="9a660-194">**Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="9a660-194">**Storage account**.</span></span> <span data-ttu-id="9a660-195">Seleccione la cuenta de almacenamiento creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9a660-195">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="9a660-196">**Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="9a660-196">**Container**.</span></span> <span data-ttu-id="9a660-197">Seleccione el contenedor creado anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="9a660-197">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="9a660-198">**Formato de serialización de eventos**.</span><span class="sxs-lookup"><span data-stu-id="9a660-198">**Event serialization format**.</span></span> <span data-ttu-id="9a660-199">Seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="9a660-199">Select **CSV**.</span></span>

    ![Configuración de la nueva entrada de trabajo](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="9a660-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9a660-201">Click **Create**.</span></span>

### <a name="configure-the-job-output"></a><span data-ttu-id="9a660-202">Configuración de la salida del trabajo</span><span class="sxs-lookup"><span data-stu-id="9a660-202">Configure the job output</span></span>
<span data-ttu-id="9a660-203">El trabajo envía los resultados al mismo almacenamiento de blobs del que obtiene la entrada.</span><span class="sxs-lookup"><span data-stu-id="9a660-203">The job sends results to the same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="9a660-204">En la opción **Topología de trabajo** de la hoja del trabajo, haga clic en el cuadro **Salidas**.</span><span class="sxs-lookup"><span data-stu-id="9a660-204">Under **Job Topology** in the job blade, click the **Outputs** box.</span></span>  
  
   ![Creación de una nueva salida para el trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="9a660-206">En la hoja **Salidas**, haga clic en **+ Agregar** y luego agregue una salida con el alias `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="9a660-206">In the **Outputs** blade, click **+ Add**, and then add an output with the alias `datamloutput`.</span></span> 

3. <span data-ttu-id="9a660-207">En **Receptor**, seleccione **Almacenamiento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="9a660-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="9a660-208">Luego rellene las demás opciones de salida con los mismos valores que usó para el almacenamiento de blobs de la entrada:</span><span class="sxs-lookup"><span data-stu-id="9a660-208">Then fill in the rest of the output settings using the same values that you used for the blob storage for input:</span></span>

    * <span data-ttu-id="9a660-209">**Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="9a660-209">**Storage account**.</span></span> <span data-ttu-id="9a660-210">Seleccione la cuenta de almacenamiento creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9a660-210">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="9a660-211">**Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="9a660-211">**Container**.</span></span> <span data-ttu-id="9a660-212">Seleccione el contenedor creado anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="9a660-212">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="9a660-213">**Formato de serialización de eventos**.</span><span class="sxs-lookup"><span data-stu-id="9a660-213">**Event serialization format**.</span></span> <span data-ttu-id="9a660-214">Seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="9a660-214">Select **CSV**.</span></span>

   ![Configuración de la nueva salida de trabajo](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="9a660-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9a660-216">Click **Create**.</span></span>   


### <a name="add-the-machine-learning-function"></a><span data-ttu-id="9a660-217">Incorporación de la función de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9a660-217">Add the Machine Learning function</span></span> 
<span data-ttu-id="9a660-218">Arriba ha publicado un modelo de Machine Learning en un servicio web.</span><span class="sxs-lookup"><span data-stu-id="9a660-218">Earlier you published a Machine Learning model to a web service.</span></span> <span data-ttu-id="9a660-219">En este escenario, cuando se ejecuta el trabajo de Stream Analysis, envía cada tweet de ejemplo de la entrada al servicio web para el análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="9a660-219">In our scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span></span> <span data-ttu-id="9a660-220">El servicio web de Machine Learning devuelve una opinión (`positive`, `neutral` o `negative`) y una probabilidad de que el tweet sea positivo.</span><span class="sxs-lookup"><span data-stu-id="9a660-220">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span></span> 

<span data-ttu-id="9a660-221">En esta sección del tutorial se define una función en el trabajo de Stream Analysis.</span><span class="sxs-lookup"><span data-stu-id="9a660-221">In this section of the tutorial, you define a function in the Stream Analysis job.</span></span> <span data-ttu-id="9a660-222">Se puede invocar a la función para enviar un tweet al servicio web y obtener la respuesta.</span><span class="sxs-lookup"><span data-stu-id="9a660-222">The function can be invoked to send a tweet to the web service and get the response back.</span></span> 

1. <span data-ttu-id="9a660-223">Asegúrese de que tiene la dirección URL y la clave de API del servicio web que ha descargado anteriormente en el libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="9a660-223">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span></span>

2. <span data-ttu-id="9a660-224">Vuelva a la hoja de información general del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a660-224">Return to the job overview blade.</span></span>

3. <span data-ttu-id="9a660-225">En **Configuración**, seleccione **Funciones** y luego haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9a660-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Adición de una función al trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="9a660-227">Escriba `sentiment` como alias de la función y rellene el resto de la hoja con estos valores:</span><span class="sxs-lookup"><span data-stu-id="9a660-227">Enter `sentiment` as the function alias and fill out the rest of the blade using these values:</span></span>

    * <span data-ttu-id="9a660-228">**Tipo de función**: seleccione **Aprendizaje automático de Azure**.</span><span class="sxs-lookup"><span data-stu-id="9a660-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="9a660-229">**Opción de importación**: seleccione **Importar de una suscripción distinta**.</span><span class="sxs-lookup"><span data-stu-id="9a660-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="9a660-230">Esto le ofrece la oportunidad de escribir la dirección URL y la clave.</span><span class="sxs-lookup"><span data-stu-id="9a660-230">This gives you a chance to enter the URL and key.</span></span>
    * <span data-ttu-id="9a660-231">**Dirección URL**: pegue la dirección URL del servicio web.</span><span class="sxs-lookup"><span data-stu-id="9a660-231">**URL**: Paste in the web service URL.</span></span>
    * <span data-ttu-id="9a660-232">**Clave**: pegue la clave de API.</span><span class="sxs-lookup"><span data-stu-id="9a660-232">**Key**: Paste in the API key.</span></span>
  
    ![Configuración para agregar una función de Machine Learning al trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="9a660-234">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9a660-234">Click **Create**.</span></span>

### <a name="create-a-query-to-transform-the-data"></a><span data-ttu-id="9a660-235">Creación de una consulta para transformar los datos</span><span class="sxs-lookup"><span data-stu-id="9a660-235">Create a query to transform the data</span></span>

<span data-ttu-id="9a660-236">Stream Analytics usa una consulta declarativa basada en SQL para examinar la entrada y procesarla.</span><span class="sxs-lookup"><span data-stu-id="9a660-236">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span></span> <span data-ttu-id="9a660-237">En esta sección se crea una consulta que lee cada tweet de entrada y luego invoca a la función de Machine Learning para llevar a cabo el análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="9a660-237">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span></span> <span data-ttu-id="9a660-238">La consulta entonces envía el resultado a la salida que se ha definido (almacenamiento de blobs).</span><span class="sxs-lookup"><span data-stu-id="9a660-238">The query then sends the result to the output that you defined (blob storage).</span></span>

1. <span data-ttu-id="9a660-239">Vuelva a la hoja de información general del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a660-239">Return to the job overview blade.</span></span>

2.  <span data-ttu-id="9a660-240">En **Topología de trabajo**, haga clic en el cuadro **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="9a660-240">Under **Job Topology**, click the **Query** box.</span></span>

    ![Creación de una consulta para el trabajo de Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="9a660-242">Escriba la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="9a660-242">Enter the following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="9a660-243">La consulta invoca a la función creada anteriormente (`sentiment`) para realizar el análisis de opiniones en cada tweet de la entrada.</span><span class="sxs-lookup"><span data-stu-id="9a660-243">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span></span> 

4. <span data-ttu-id="9a660-244">Haga clic en **Guardar** para guardar la consulta.</span><span class="sxs-lookup"><span data-stu-id="9a660-244">Click **Save** to save the query.</span></span>


## <a name="start-the-stream-analytics-job-and-check-the-output"></a><span data-ttu-id="9a660-245">Inicio del trabajo de Stream Analytics y consulta de la salida</span><span class="sxs-lookup"><span data-stu-id="9a660-245">Start the Stream Analytics job and check the output</span></span>

<span data-ttu-id="9a660-246">Ya se puede iniciar el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9a660-246">You can now start the Stream Analytics job.</span></span>

### <a name="start-the-job"></a><span data-ttu-id="9a660-247">Inicio del trabajo</span><span class="sxs-lookup"><span data-stu-id="9a660-247">Start the job</span></span>
1. <span data-ttu-id="9a660-248">Vuelva a la hoja de información general del trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a660-248">Return to the job overview blade.</span></span>

2. <span data-ttu-id="9a660-249">Haga clic en **Iniciar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="9a660-249">Click **Start** at the top of the blade.</span></span>

    ![Creación de una consulta para el trabajo de Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="9a660-251">En **Iniciar trabajo**, seleccione **Personalizado** y luego seleccione un día antes de la fecha de carga del archivo CSV en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9a660-251">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span></span> <span data-ttu-id="9a660-252">Cuando haya terminado, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9a660-252">When you're done, click **Start**.</span></span>  


### <a name="check-the-output"></a><span data-ttu-id="9a660-253">Consulta de la salida</span><span class="sxs-lookup"><span data-stu-id="9a660-253">Check the output</span></span>
1. <span data-ttu-id="9a660-254">Deje que el trabajo se ejecute durante unos minutos hasta que vea actividad en el cuadro **Supervisión**.</span><span class="sxs-lookup"><span data-stu-id="9a660-254">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span></span> 

2. <span data-ttu-id="9a660-255">Si tiene alguna herramienta que suela usar para examinar el contenido del almacenamiento de blobs, úsela para examinar el contenedor `azuresamldemoblob`.</span><span class="sxs-lookup"><span data-stu-id="9a660-255">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span></span> <span data-ttu-id="9a660-256">También puede realizar los siguientes pasos en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="9a660-256">Alternatively, do the following steps in the Azure portal:</span></span>

    1. <span data-ttu-id="9a660-257">En el portal, busque la cuenta de almacenamiento `samldemo` y, en ella, busque el contenedor `azuresamldemoblob`.</span><span class="sxs-lookup"><span data-stu-id="9a660-257">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span></span> <span data-ttu-id="9a660-258">En el contenedor verá dos archivos: el que contiene los tweets de ejemplo y un archivo CSV generado por el trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9a660-258">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span></span>
    2. <span data-ttu-id="9a660-259">Haga clic con el botón derecho en el archivo generado y luego seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="9a660-259">Right-click the generated file and then select **Download**.</span></span> 

   ![Descarga de la salida del trabajo CSV desde el almacenamiento de blobs](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="9a660-261">Abra el archivo CSV generado.</span><span class="sxs-lookup"><span data-stu-id="9a660-261">Open the generated CSV file.</span></span> <span data-ttu-id="9a660-262">Verá algo parecido al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a660-262">You see something like the following example:</span></span>  
   
   ![Aprendizaje automático de Análisis de transmisiones, vista CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="9a660-264">Visualización de métricas</span><span class="sxs-lookup"><span data-stu-id="9a660-264">View metrics</span></span>
<span data-ttu-id="9a660-265">También puede observar las métricas relacionadas con la función de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a660-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="9a660-266">Las siguientes métricas relacionadas con la función se muestran en el cuadro **Supervisión** de la hoja de trabajo:</span><span class="sxs-lookup"><span data-stu-id="9a660-266">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span></span>

* <span data-ttu-id="9a660-267">**Solicitudes de función** indica el número de solicitudes enviadas al servicio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9a660-267">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="9a660-268">**Eventos de la función** indica el número de eventos de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="9a660-268">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="9a660-269">De forma predeterminada, cada solicitud de un servicio web Machine Learning contiene hasta 1000 eventos.</span><span class="sxs-lookup"><span data-stu-id="9a660-269">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="9a660-270">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a660-270">Next steps</span></span>

* [<span data-ttu-id="9a660-271">Introducción al Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="9a660-271">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9a660-272">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="9a660-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9a660-273">Integración de la API de REST y Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9a660-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="9a660-274">Referencia de API de REST de administración de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="9a660-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



