---
title: "aaaStream datos de análisis de transmisiones en el almacén de Data Lake | Documentos de Microsoft"
description: "Usar datos de análisis de transmisiones de Azure toostream en almacén de Azure Data Lake"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="e0d3c-103">Transmisión de datos del blob de Almacenamiento de Azure al Almacén de Data Lake mediante el Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="e0d3c-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="e0d3c-104">En este artículo, aprenderá cómo toouse Azure Data Lake almacenar como una salida para un trabajo de análisis de transmisiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="e0d3c-105">Este artículo muestra un escenario sencillo que lee los datos de un blob de almacenamiento de Azure (entrada) y escrituras Hola almacén data Lake de tooData (salida).</span><span class="sxs-lookup"><span data-stu-id="e0d3c-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="e0d3c-106">En este momento, la creación y configuración de almacén de Data Lake genera para el análisis de transmisiones solo se admite en hello [Portal clásico de Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e0d3c-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="e0d3c-107">Por lo tanto, algunas partes de este tutorial usará Hola Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="e0d3c-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e0d3c-108">Prerequisites</span></span>
<span data-ttu-id="e0d3c-109">Antes de comenzar este tutorial, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e0d3c-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="e0d3c-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-110">**An Azure subscription**.</span></span> <span data-ttu-id="e0d3c-111">Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0d3c-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="e0d3c-112">**Cuenta de Almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-112">**Azure Storage account**.</span></span> <span data-ttu-id="e0d3c-113">Usará un contenedor de blob desde estos datos de tooinput de cuenta para un trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="e0d3c-114">Para este tutorial, suponga que tiene una cuenta de almacenamiento denominada **storageforasa** y llama a un contenedor dentro de la cuenta de hello **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="e0d3c-115">Una vez haya creado el contenedor de hello, cargue un tooit de archivo de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="e0d3c-116">**Cuenta del Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="e0d3c-117">Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e0d3c-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="e0d3c-118">Supongamos que tiene una cuenta de Data Lake Store llamada **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="e0d3c-119">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="e0d3c-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="e0d3c-120">Primero debe crear un trabajo de Análisis de transmisiones que incluya un origen de entrada y un destino de salida.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="e0d3c-121">Para este tutorial, origen de hello es un contenedor de blobs de Azure y destino de hello es el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="e0d3c-122">Inicio de sesión toohello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0d3c-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e0d3c-123">En el panel izquierdo de hello, haga clic en **trabajos de análisis de transmisiones**y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="e0d3c-124">![Creación de un trabajo de Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Creación de un trabajo de Stream Analytics")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="e0d3c-125">Asegúrese de que se crea el trabajo en hello misma región que la cuenta de almacenamiento de Hola o se incurrirá en costos adicionales de mover datos entre regiones.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="e0d3c-126">Creación de una entrada de Blob para trabajo Hola</span><span class="sxs-lookup"><span data-stu-id="e0d3c-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="e0d3c-127">Página de Hola abierto para el trabajo de análisis de transmisiones de hello, en el panel izquierdo de hello, haga clic en hello **entradas** ficha y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="e0d3c-128">![Agregar un trabajo de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "agregar un trabajo de entrada tooyour")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="e0d3c-129">En hello **nueva entrada** hoja, proporcionar Hola después de valores.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="e0d3c-130">![Agregar un trabajo de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "agregar un trabajo de entrada tooyour")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="e0d3c-131">Para **alias de entrada**, escriba un nombre único para la entrada de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="e0d3c-132">En **Source type** (Tipo de origen), seleccione **Flujo de datos**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="e0d3c-133">En **Origen**, seleccione **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="e0d3c-134">En **Suscripción**, seleccione **Usar almacenamiento de blobs de la suscripción actual**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="e0d3c-135">Para **cuenta de almacenamiento**, seleccione la cuenta de almacenamiento de Hola que creó como parte de los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="e0d3c-136">Para **contenedor**, seleccione contenedor Hola que creó en hello seleccionado cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="e0d3c-137">En **Formato de serialización de eventos**, seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="e0d3c-138">En **Delimitador**, seleccione **tabulación**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="e0d3c-139">En **Codificación**, seleccione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="e0d3c-140">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-140">Click **Create**.</span></span> <span data-ttu-id="e0d3c-141">portal Hola ahora agrega la entrada de Hola y Hola tooit de conexión de prueba.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="e0d3c-142">Crear una salida de almacén de Data Lake para trabajo Hola</span><span class="sxs-lookup"><span data-stu-id="e0d3c-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="e0d3c-143">Abrir página hello para el trabajo de análisis de transmisiones de hello, haga clic en hello **salidas** ficha y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="e0d3c-144">![Agregar un trabajo de salida tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "agregar un trabajo de tooyour de salida")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="e0d3c-145">En hello **nueva salida** hoja, proporcionar Hola después de valores.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="e0d3c-146">![Agregar un trabajo de salida tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "agregar un trabajo de tooyour de salida")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="e0d3c-147">Para **alias de salida**, escriba un un nombre único para la salida del trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="e0d3c-148">Se trata de un nombre descriptivo que se usa en consultas toodirect Hola consulta salida toothis almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="e0d3c-149">En **Receptor**, seleccione **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="e0d3c-150">Podrá tooauthorize solicitada tener acceso a la cuenta de almacén de tooData Lake.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="e0d3c-151">Haga clic en **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="e0d3c-152">En hello **nueva salida** hoja, continuar hello tooprovide después de valores.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="e0d3c-153">![Agregar un trabajo de salida tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "agregar un trabajo de tooyour de salida")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="e0d3c-154">Para **nombre de la cuenta**, seleccione cuenta del almacén de Data Lake de Hola que ya haya creado en la que desea toobe de salida de hello trabajo enviado a.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="e0d3c-155">Para **modelo de prefijo de ruta de acceso**, escriba un toowrite de ruta de archivo especifican de los archivos dentro de hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="e0d3c-156">Para **formato de fecha**, si usó un token de fecha en la ruta de acceso de prefijo de hello, puede seleccionar el formato de fecha de hello en el que se organizan los archivos.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="e0d3c-157">Para **formato de hora**, si se usa un símbolo (token) de tiempo en la ruta de acceso de prefijo de hello, especifique el formato de hora de hello en el que se organizan los archivos.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="e0d3c-158">En **Formato de serialización de eventos**, seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="e0d3c-159">En **Delimitador**, seleccione **tabulación**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="e0d3c-160">En **Codificación**, seleccione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="e0d3c-161">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-161">Click **Create**.</span></span> <span data-ttu-id="e0d3c-162">portal de Hello ahora agrega la salida de hello y prueba Hola conexión tooit.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="e0d3c-163">Ejecutar trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="e0d3c-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="e0d3c-164">toorun un trabajo de análisis de transmisiones, debe ejecutar una consulta de hello **consulta** ficha. Para este tutorial, puede ejecutar la consulta de ejemplo de Hola reemplazando los marcadores de posición de hello con hello trabajo alias de entrada y salidos, como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="e0d3c-165">![Ejecución de una consulta](./media/data-lake-store-stream-analytics/run.query.png "Ejecución de una consulta")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="e0d3c-166">Haga clic en **guardar** desde la parte superior de Hola de pantalla de bienvenida y, a continuación, desde hello **Introducción** , haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="e0d3c-167">En el cuadro de diálogo de hello, seleccione **tiempo personalizada**y, a continuación, establezca Hola fecha y hora actuales.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="e0d3c-168">![Establecimiento de la hora del trabajo](./media/data-lake-store-stream-analytics/run.query.2.png "Establecimiento de la hora del trabajo")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="e0d3c-169">Haga clic en **iniciar** trabajo de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="e0d3c-170">Puede pasar hasta el trabajo hello toostart de tooa dos minutos.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="e0d3c-171">datos tootrigger Hola trabajo toopick Hola de blob de hello, copie un contenedor de blobs ejemplo toohello de archivo de datos.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="e0d3c-172">Puede obtener un archivo de datos de ejemplo de Hola [repositorio de Git de Azure datos Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="e0d3c-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="e0d3c-173">Para este tutorial, vamos a copiar archivo hello **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="e0d3c-174">Puede usar varios clientes, como [Azure Storage Explorer](http://storageexplorer.com/), contenedor de blobs de tooupload datos tooa.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="e0d3c-175">De hello **Introducción** ficha **supervisión**, vea cómo se procesan los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="e0d3c-176">![Supervisión de trabajos](./media/data-lake-store-stream-analytics/run.query.3.png "Supervisión de trabajos")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="e0d3c-177">Por último, puede comprobar que datos de salida del trabajo de hello están disponibles en la cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="e0d3c-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="e0d3c-178">![Comprobación de la salida](./media/data-lake-store-stream-analytics/run.query.4.png "Comprobación de la salida")</span><span class="sxs-lookup"><span data-stu-id="e0d3c-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="e0d3c-179">En el panel de exploración de datos de hello, observar que hello como resultado escrito tooa la ruta de acceso de carpeta como especificado en hello opciones de salida de almacén de Data Lake (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="e0d3c-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="e0d3c-180">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e0d3c-180">See also</span></span>
* [<span data-ttu-id="e0d3c-181">Crear un toouse de clúster de HDInsight almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="e0d3c-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
