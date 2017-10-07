---
title: "aaaAzure integración de análisis de transmisiones y aprendizaje automático | Documentos de Microsoft"
description: "¿Cómo toouse una función definida por el usuario y el aprendizaje automático en un trabajo de análisis de transmisiones"
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
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="15d15-103">Análisis de opiniones mediante Azure Stream Analytics y Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15d15-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="15d15-104">Este artículo describe cómo tooquickly configura un simple trabajo de análisis de transmisiones de Azure que integra el aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="15d15-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="15d15-105">Usan un modelo de análisis de opiniones de aprendizaje automático de hello datos de texto de la Galería de inteligencia de Cortana tooanalyze transmisión por secuencias y determinar la puntuación de opinión de hello en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="15d15-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="15d15-106">Hola Cortana Intelligence Suite permite realizar esta tarea sin preocuparse por las complejidades de saludo de la creación de un modelo de análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="15d15-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="15d15-107">Puede aplicar lo que aprenda de este tooscenarios artículo como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="15d15-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="15d15-108">Análisis de opiniones en tiempo real en datos de Twitter que se están transmitiendo.</span><span class="sxs-lookup"><span data-stu-id="15d15-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="15d15-109">Análisis de registros de chats de clientes con el personal de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="15d15-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="15d15-110">Evaluación de comentarios en foros, blogs y vídeos.</span><span class="sxs-lookup"><span data-stu-id="15d15-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="15d15-111">Muchos otros escenarios de puntuación predictiva en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="15d15-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="15d15-112">En un escenario real, obtendría datos Hola directamente desde un flujo de datos de Twitter.</span><span class="sxs-lookup"><span data-stu-id="15d15-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="15d15-113">tutorial de hello toosimplify, hemos escrito, por lo que hello trabajo de análisis de transmisión por secuencias obtiene tweets desde un archivo CSV en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="15d15-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="15d15-114">Puede crear su propio archivo CSV, o puede usar un archivo CSV de ejemplo, como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="15d15-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![tweets de ejemplo de un archivo CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="15d15-116">trabajo de análisis de transmisión por secuencias de Hola que cree aplica modelo de análisis de opiniones hello como una función definida por el usuario (UDF) en los datos de texto de ejemplo de Hola de almacén de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="15d15-117">salida de Hello (resultado de hello de análisis de opiniones Hola) se escribe toohello mismo almacén de blob en un archivo CSV diferente.</span><span class="sxs-lookup"><span data-stu-id="15d15-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="15d15-118">Hello en la ilustración siguiente se muestra esta configuración.</span><span class="sxs-lookup"><span data-stu-id="15d15-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="15d15-119">Como se ha indicado, para un escenario más realista, puede sustituir el almacenamiento de blobs por datos de Twitter que se estén transmitiendo desde una entrada de Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="15d15-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="15d15-120">Además, puede generar un [Microsoft Power BI](https://powerbi.microsoft.com/) visualización en tiempo real de opiniones agregado Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Información general sobre la integración de Stream Analytics Machine Learning](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="15d15-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="15d15-122">Prerequisites</span></span>
<span data-ttu-id="15d15-123">Antes de empezar, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="15d15-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="15d15-124">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="15d15-124">An active Azure subscription.</span></span>
* <span data-ttu-id="15d15-125">Un archivo CSV con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="15d15-125">A CSV file with some data in it.</span></span> <span data-ttu-id="15d15-126">Puede descargar archivo hello mostrado anteriormente desde [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), o bien puede crear su propio archivo.</span><span class="sxs-lookup"><span data-stu-id="15d15-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="15d15-127">En este artículo, se supone que está usando el archivo hello desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="15d15-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="15d15-128">En un nivel alto, tareas de hello toocomplete que se explican en este artículo, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="15d15-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="15d15-129">Crear una cuenta de almacenamiento de Azure y un contenedor de almacenamiento de blobs y cargue un contenedor de toohello del archivo de entrada con formato CSV.</span><span class="sxs-lookup"><span data-stu-id="15d15-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="15d15-130">Agregar un modelo de análisis de opiniones de área de trabajo de aprendizaje automático de Azure de hello Cortana Intelligence Galería tooyour e implementar este modelo como un servicio web en el área de trabajo de aprendizaje automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="15d15-131">Crear un trabajo de análisis de transmisiones que llama a este servicio web como una función en las opiniones de orden toodetermine Hola entrada de texto.</span><span class="sxs-lookup"><span data-stu-id="15d15-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="15d15-132">Iniciar el trabajo de análisis de transmisiones de Hola y compruebe la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="15d15-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="15d15-133">Crear un contenedor de almacenamiento y cargar el archivo de entrada de hello CSV</span><span class="sxs-lookup"><span data-stu-id="15d15-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="15d15-134">Para este paso, puede usar cualquier archivo CSV, como Hola uno disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="15d15-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="15d15-135">Hola portal de Azure, haga clic en **New** &gt; **almacenamiento** &gt; **cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="15d15-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![creación de una nueva cuenta de almacenamiento](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="15d15-137">Proporcione un nombre (`samldemo` en el ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="15d15-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="15d15-138">nombre de Hello puede usar solo letras minúsculas y números, y debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="15d15-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="15d15-139">Especifique un grupo de recursos existente y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="15d15-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="15d15-140">Para la ubicación, se recomienda que todos los recursos de hello creados en este tutorial, use Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="15d15-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![especificación de los detalles de la cuenta de almacenamiento](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="15d15-142">Hola portal de Azure, seleccione la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="15d15-143">En la hoja de la cuenta de almacenamiento de hello, haga clic en **contenedores** y, a continuación, haga clic en  **+ &nbsp;contenedor** toocreate el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="15d15-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![creación de contenedor de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="15d15-145">Proporcione un nombre para el contenedor de hello (`azuresamldemoblob` en el ejemplo de Hola) y compruebe que **tipo de acceso** se establece demasiado**Blob**.</span><span class="sxs-lookup"><span data-stu-id="15d15-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="15d15-146">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="15d15-146">When you're done, click **OK**.</span></span>

    ![especificación de los detalles del contenedor de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="15d15-148">Hola **contenedores** hoja, seleccione Hola nuevo contenedor de, que abre una hoja de Hola para ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="15d15-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="15d15-149">Haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="15d15-149">Click **Upload**.</span></span>

    ![botón "Cargar" de un contenedor](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="15d15-151">Hola **cargar blob** hoja, especifique el archivo CSV de Hola que quiere toouse de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="15d15-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="15d15-152">Para **tipo de Blob**, seleccione **blob en bloques** y conjunto Hola bloque tamaño too4 MB, que es suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="15d15-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![carga del archivo de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="15d15-154">Haga clic en hello **cargar** situado en parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="15d15-155">Agregar modelos de análisis de opiniones Hola de hello Galería de inteligencia de Cortana</span><span class="sxs-lookup"><span data-stu-id="15d15-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="15d15-156">Ahora que los datos de ejemplo de Hola están en un blob, puede habilitar el modelo de análisis de opiniones hello en Galería de inteligencia de Cortana.</span><span class="sxs-lookup"><span data-stu-id="15d15-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="15d15-157">Vaya toohello [modelo de análisis predictivo opiniones](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) página Hola Galería de inteligencia de Cortana.</span><span class="sxs-lookup"><span data-stu-id="15d15-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="15d15-158">Haga clic en **Abrir en Studio**.</span><span class="sxs-lookup"><span data-stu-id="15d15-158">Click **Open in Studio**.</span></span>  
   
   ![Aprendizaje automático de Análisis de transmisiones, abrir Aprendizaje automático](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="15d15-160">Inicie sesión en el área de trabajo de toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="15d15-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="15d15-161">Seleccione una ubicación.</span><span class="sxs-lookup"><span data-stu-id="15d15-161">Select a location.</span></span>

4. <span data-ttu-id="15d15-162">Haga clic en **ejecutar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="15d15-163">se ejecuta el proceso de Hello, que tarda aproximadamente un minuto.</span><span class="sxs-lookup"><span data-stu-id="15d15-163">hello process runs, which takes about a minute.</span></span>

   ![ejecución del experimento en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="15d15-165">Después de que se ejecute correctamente el proceso de hello, seleccione **implementar el servicio de Web** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![implementación del experimento como un servicio web en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="15d15-167">toovalidate que Hola opiniones modelo de análisis es toouse listo, haga clic en hello **prueba** botón.</span><span class="sxs-lookup"><span data-stu-id="15d15-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="15d15-168">Proporcione algún texto de entrada, como "Me encanta Microsoft".</span><span class="sxs-lookup"><span data-stu-id="15d15-168">Provide text input such as "I love Microsoft".</span></span> 

   ![prueba del experimento en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="15d15-170">Si prueba Hola funciona, verá un toohello similar de resultados siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="15d15-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![resultados de la prueba en Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="15d15-172">Hola **aplicaciones** columna, haga clic en hello **Excel 2010 o el libro anterior** toodownload vínculo un libro de Excel.</span><span class="sxs-lookup"><span data-stu-id="15d15-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="15d15-173">libro de Hello contiene clave Hola una API y la dirección URL de Hola que necesite tooset más adelante el trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Aprendizaje automático de Análisis de transmisiones, vista rápida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="15d15-175">Crear un trabajo de análisis de transmisiones que usa el modelo de aprendizaje automático de Hola</span><span class="sxs-lookup"><span data-stu-id="15d15-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="15d15-176">Ahora puede crear un trabajo de análisis de transmisiones que lee tweets de ejemplo de Hola desde archivo CSV de hello en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="15d15-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="15d15-177">Crear trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="15d15-177">Create hello job</span></span>

1. <span data-ttu-id="15d15-178">Vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15d15-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="15d15-179">Haga clic en **Nuevo** > **Internet de las cosas** > **Trabajo de Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="15d15-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Ruta de acceso del portal Azure para obtener tooa nuevo trabajo de análisis de transmisiones](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="15d15-181">Nombre de trabajo de hello `azure-sa-ml-demo`, especifique una suscripción, especificar un grupo de recursos existente o cree uno nuevo y seleccione ubicación hello para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![especificación de la configuración del nuevo trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="15d15-183">Configurar entrada de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="15d15-183">Configure hello job input</span></span>
<span data-ttu-id="15d15-184">trabajo de Hello obtiene su entrada desde archivo CSV de Hola que carga de almacenamiento de tooblob anterior.</span><span class="sxs-lookup"><span data-stu-id="15d15-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="15d15-185">Después de que se ha creado un trabajo de hello, en **trabajo topología** en la hoja de trabajo de hello, haga clic en hello **entradas** cuadro.</span><span class="sxs-lookup"><span data-stu-id="15d15-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![cuadro "Entradas" de la hoja del trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="15d15-187">Hola **entradas** hoja, haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="15d15-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   !['Add' botón para agregar un trabajo de análisis de transmisiones de entrada toohello](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="15d15-189">Rellene hello **nueva entrada** hoja con estos valores:</span><span class="sxs-lookup"><span data-stu-id="15d15-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="15d15-190">**Alias de entrada**: usar el nombre de hello `datainput`.</span><span class="sxs-lookup"><span data-stu-id="15d15-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="15d15-191">**Tipo de origen**: seleccione **Flujo de datos**.</span><span class="sxs-lookup"><span data-stu-id="15d15-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="15d15-192">**Origen**: seleccione **Almacenamiento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="15d15-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="15d15-193">**Opción de importación**: seleccione **Usar almacenamiento de blobs de la suscripción actual**.</span><span class="sxs-lookup"><span data-stu-id="15d15-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="15d15-194">**Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="15d15-194">**Storage account**.</span></span> <span data-ttu-id="15d15-195">Seleccione la cuenta de almacenamiento de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="15d15-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="15d15-196">**Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="15d15-196">**Container**.</span></span> <span data-ttu-id="15d15-197">Contenedor de hello SELECT que creó anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="15d15-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="15d15-198">**Formato de serialización de eventos**.</span><span class="sxs-lookup"><span data-stu-id="15d15-198">**Event serialization format**.</span></span> <span data-ttu-id="15d15-199">Seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="15d15-199">Select **CSV**.</span></span>

    ![Configuración de la nueva entrada de trabajo](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="15d15-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="15d15-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="15d15-202">Configurar la salida de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="15d15-202">Configure hello job output</span></span>
<span data-ttu-id="15d15-203">Hola trabajo envía resultados toohello mismo donde se obtiene información de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="15d15-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="15d15-204">En **trabajo topología** en la hoja de trabajo de hello, haga clic en hello **salidas** cuadro.</span><span class="sxs-lookup"><span data-stu-id="15d15-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Creación de una nueva salida para el trabajo de Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="15d15-206">Hola **salidas** hoja, haga clic en **+ agregar**y, a continuación, agregar una salida con el alias de hello `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="15d15-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="15d15-207">En **Receptor**, seleccione **Almacenamiento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="15d15-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="15d15-208">Relleno a continuación, en el resto de Hola de hello salida configuración mediante Hola mismos valores que se usa para el almacenamiento de blobs de hello para la entrada:</span><span class="sxs-lookup"><span data-stu-id="15d15-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="15d15-209">**Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="15d15-209">**Storage account**.</span></span> <span data-ttu-id="15d15-210">Seleccione la cuenta de almacenamiento de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="15d15-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="15d15-211">**Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="15d15-211">**Container**.</span></span> <span data-ttu-id="15d15-212">Contenedor de hello SELECT que creó anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="15d15-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="15d15-213">**Formato de serialización de eventos**.</span><span class="sxs-lookup"><span data-stu-id="15d15-213">**Event serialization format**.</span></span> <span data-ttu-id="15d15-214">Seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="15d15-214">Select **CSV**.</span></span>

   ![Configuración de la nueva salida de trabajo](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="15d15-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="15d15-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="15d15-217">Agregar la función de aprendizaje automático de hello</span><span class="sxs-lookup"><span data-stu-id="15d15-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="15d15-218">Anteriormente se publica un servicio web de aprendizaje automático modelo tooa.</span><span class="sxs-lookup"><span data-stu-id="15d15-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="15d15-219">En nuestro escenario, cuando se ejecuta el trabajo de análisis de secuencia de hello, envía cada tweet de ejemplo de servicio de web de entrada toohello Hola para análisis de opiniones.</span><span class="sxs-lookup"><span data-stu-id="15d15-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="15d15-220">Hola servicio web de aprendizaje automático devuelve una opinión (`positive`, `neutral`, o `negative`) y una probabilidad de tweet Hola está positivo.</span><span class="sxs-lookup"><span data-stu-id="15d15-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="15d15-221">En esta sección del tutorial de hello, definir una función de trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="15d15-222">función Hello pueda ser invocado toosend un servicio web de toohello de tweet y obtener respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="15d15-223">Asegúrese de que tiene Hola dirección URL y la API de clave de servicio web que ha descargado anteriormente en el libro de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="15d15-224">Hoja de información general del trabajo toohello devuelto.</span><span class="sxs-lookup"><span data-stu-id="15d15-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="15d15-225">En **Configuración**, seleccione **Funciones** y luego haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="15d15-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Agregar un trabajo de análisis de transmisiones de toohello (función)](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="15d15-227">Escriba `sentiment` como Hola función alias y rellene rest Hola de hoja de hello con estos valores:</span><span class="sxs-lookup"><span data-stu-id="15d15-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="15d15-228">**Tipo de función**: seleccione **Aprendizaje automático de Azure**.</span><span class="sxs-lookup"><span data-stu-id="15d15-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="15d15-229">**Opción de importación**: seleccione **Importar de una suscripción distinta**.</span><span class="sxs-lookup"><span data-stu-id="15d15-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="15d15-230">Esto proporciona una oportunidad tooenter Hola URL y una clave.</span><span class="sxs-lookup"><span data-stu-id="15d15-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="15d15-231">**Dirección URL**: pegar Hola URL del servicio web.</span><span class="sxs-lookup"><span data-stu-id="15d15-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="15d15-232">**Clave**: pegar en la clave de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-232">**Key**: Paste in hello API key.</span></span>
  
    ![Configuración para agregar un trabajo de análisis de transmisiones de toohello de función de aprendizaje automático](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="15d15-234">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="15d15-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="15d15-235">Crear una consulta de datos de hello tootransform</span><span class="sxs-lookup"><span data-stu-id="15d15-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="15d15-236">Análisis de transmisiones usa una entrada de consulta declarativa basado en SQL tooexamine hello y procesarlo.</span><span class="sxs-lookup"><span data-stu-id="15d15-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="15d15-237">En esta sección, creará una consulta que lee cada tweet de entrada y, a continuación, se llama a análisis de opiniones de tooperform de función de aprendizaje automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="15d15-238">consulta de Hello, a continuación, envía Hola resultado toohello de salida que definió (almacenamiento de blobs).</span><span class="sxs-lookup"><span data-stu-id="15d15-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="15d15-239">Hoja de información general del trabajo toohello devuelto.</span><span class="sxs-lookup"><span data-stu-id="15d15-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="15d15-240">En **trabajo topología**, haga clic en hello **consulta** cuadro.</span><span class="sxs-lookup"><span data-stu-id="15d15-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Creación de una consulta para el trabajo de Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="15d15-242">Escriba Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="15d15-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="15d15-243">consulta de Hello invoca la función hello que creó anteriormente (`sentiment`) en el análisis de opiniones tooperform de orden en cada tweet en la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="15d15-244">Haga clic en **guardar** consulta de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="15d15-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="15d15-245">Iniciar el trabajo de análisis de transmisiones de Hola y compruebe la salida de hello</span><span class="sxs-lookup"><span data-stu-id="15d15-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="15d15-246">Ahora puede iniciar el trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="15d15-247">Iniciar el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="15d15-247">Start hello job</span></span>
1. <span data-ttu-id="15d15-248">Hoja de información general del trabajo toohello devuelto.</span><span class="sxs-lookup"><span data-stu-id="15d15-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="15d15-249">Haga clic en **iniciar** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-249">Click **Start** at hello top of hello blade.</span></span>

    ![Creación de una consulta para el trabajo de Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="15d15-251">Hola **Start job**, seleccione **personalizada**y, a continuación, seleccione un día toowhen anterior que cargó el almacenamiento de información de hello CSV archivo tooblob.</span><span class="sxs-lookup"><span data-stu-id="15d15-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="15d15-252">Cuando haya terminado, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="15d15-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="15d15-253">Compruebe la salida de hello</span><span class="sxs-lookup"><span data-stu-id="15d15-253">Check hello output</span></span>
1. <span data-ttu-id="15d15-254">Trabajo de hello permiten ejecutar durante varios minutos hasta que vea actividad Hola **supervisión** cuadro.</span><span class="sxs-lookup"><span data-stu-id="15d15-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="15d15-255">Si tiene una herramienta que suele usar el contenido de hello tooexamine de almacenamiento de blobs, use ese Hola de tooexamine herramienta `azuresamldemoblob` contenedor.</span><span class="sxs-lookup"><span data-stu-id="15d15-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="15d15-256">Como alternativa, Hola pasos de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="15d15-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="15d15-257">En el portal de hello, busque hello `samldemo` almacenamiento de la cuenta y, dentro de la cuenta de hello, buscar hello `azuresamldemoblob` contenedor.</span><span class="sxs-lookup"><span data-stu-id="15d15-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="15d15-258">Verá dos archivos en el contenedor de hello: Hola archivo que contenga tweets de ejemplo de Hola y un archivo CSV generado por el trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="15d15-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="15d15-259">Haga clic en archivo hello generado y, a continuación, seleccione **descargar**.</span><span class="sxs-lookup"><span data-stu-id="15d15-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Descarga de la salida del trabajo CSV desde el almacenamiento de blobs](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="15d15-261">Abra Hola genera el archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="15d15-261">Open hello generated CSV file.</span></span> <span data-ttu-id="15d15-262">Verá algo parecido a Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="15d15-262">You see something like hello following example:</span></span>  
   
   ![Aprendizaje automático de Análisis de transmisiones, vista CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="15d15-264">Visualización de métricas</span><span class="sxs-lookup"><span data-stu-id="15d15-264">View metrics</span></span>
<span data-ttu-id="15d15-265">También puede observar las métricas relacionadas con la función de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="15d15-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="15d15-266">Hola siguiendo las métricas relacionadas con la función se muestra en hello **supervisión** cuadro en la hoja de trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="15d15-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="15d15-267">**Función solicitudes** indica Hola número de solicitudes enviadas tooa servicio web de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="15d15-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="15d15-268">**Función eventos** indica el número de Hola de eventos de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="15d15-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="15d15-269">De forma predeterminada, cada servicio web de aprendizaje automático de tooa de solicitud contiene una too1, 000 eventos.</span><span class="sxs-lookup"><span data-stu-id="15d15-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="15d15-270">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15d15-270">Next steps</span></span>

* [<span data-ttu-id="15d15-271">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="15d15-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="15d15-272">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="15d15-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="15d15-273">Integración de la API de REST y Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15d15-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="15d15-274">Referencia de API de REST de administración de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="15d15-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



