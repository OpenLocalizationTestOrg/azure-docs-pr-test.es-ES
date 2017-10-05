---
title: "Transmisión de datos de Stream Analytics a Data Lake Store| Microsoft Docs"
description: "Uso de Análisis de transmisiones para transmitir datos en el Almacén de Azure Data Lake"
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
ms.openlocfilehash: 90104aaacf24a5a7156900fc3848a27f60329814
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="35bb7-103">Transmisión de datos del blob de Almacenamiento de Azure al Almacén de Data Lake mediante el Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="35bb7-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="35bb7-104">En este artículo aprenderá a utilizar el Almacén de Azure Data Lake como salida para un trabajo de Análisis de transmisiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="35bb7-104">In this article you will learn how to use Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="35bb7-105">Este artículo muestra un escenario simple que lee datos desde un blob de Almacenamiento de Azure (entrada) y los escribe en el Almacén de Data Lake (salida).</span><span class="sxs-lookup"><span data-stu-id="35bb7-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes the data to Data Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="35bb7-106">En este momento, la creación y la configuración de salidas de Data Lake Store para Análisis de transmisiones solo se admiten en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="35bb7-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in the [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="35bb7-107">Por lo tanto, algunas partes de este tutorial usarán el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="35bb7-107">Hence, some parts of this tutorial will use the Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="35bb7-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="35bb7-108">Prerequisites</span></span>
<span data-ttu-id="35bb7-109">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="35bb7-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="35bb7-110">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-110">**An Azure subscription**.</span></span> <span data-ttu-id="35bb7-111">Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35bb7-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="35bb7-112">**Cuenta de Almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-112">**Azure Storage account**.</span></span> <span data-ttu-id="35bb7-113">Usará un contenedor de blobs desde esta cuenta para introducir datos en un trabajo de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="35bb7-113">You will use a blob container from this account to input data for a Stream Analytics job.</span></span> <span data-ttu-id="35bb7-114">En este tutorial, se asume que tiene una cuenta de almacenamiento denominada **storageforasa** y un contenedor dentro de la cuenta denominado **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within the account called **storageforasacontainer**.</span></span> <span data-ttu-id="35bb7-115">Una vez creado el contenedor, va a cargar un archivo de datos de ejemplo en él.</span><span class="sxs-lookup"><span data-stu-id="35bb7-115">Once you have created the container, upload a sample data file to it.</span></span> 
  
* <span data-ttu-id="35bb7-116">**Cuenta del Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="35bb7-117">Siga las instrucciones que se describen en [Introducción al Almacén de Azure Data Lake mediante el Portal de Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35bb7-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="35bb7-118">Supongamos que tiene una cuenta de Data Lake Store llamada **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="35bb7-119">Creación de un trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="35bb7-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="35bb7-120">Primero debe crear un trabajo de Análisis de transmisiones que incluya un origen de entrada y un destino de salida.</span><span class="sxs-lookup"><span data-stu-id="35bb7-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="35bb7-121">Para este tutorial, el origen es un contenedor de blobs de Azure y el destino es el Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35bb7-121">For this tutorial, the source is an Azure blob container and the destination is Data Lake Store.</span></span>

1. <span data-ttu-id="35bb7-122">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="35bb7-122">Sign on to the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="35bb7-123">En el panel izquierdo, haga clic en **Trabajos de Stream Analytics** y luego haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-123">From the left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="35bb7-124">![Creación de un trabajo de Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Creación de un trabajo de Stream Analytics")</span><span class="sxs-lookup"><span data-stu-id="35bb7-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="35bb7-125">Asegúrese de crear el trabajo en la misma región que la cuenta de almacenamiento o incurrirá en costos adicionales derivados de mover datos entre regiones.</span><span class="sxs-lookup"><span data-stu-id="35bb7-125">Make sure you create job in the same region as the storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-the-job"></a><span data-ttu-id="35bb7-126">Creación de una entrada de blob para el trabajo</span><span class="sxs-lookup"><span data-stu-id="35bb7-126">Create a Blob input for the job</span></span>

1. <span data-ttu-id="35bb7-127">Abra la página del trabajo de Stream Analytics y en el panel izquierdo haga clic en la pestaña **Inputs** (Entradas) y luego haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-127">Open the page for the Stream Analytics job, from the left pane click the **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="35bb7-128">![Adición de una entrada al trabajo](./media/data-lake-store-stream-analytics/create.input.1.png "Adición de una entrada al trabajo")</span><span class="sxs-lookup"><span data-stu-id="35bb7-128">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input to your job")</span></span>

2. <span data-ttu-id="35bb7-129">En la hoja **Nueva entrada**, proporcione los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="35bb7-129">On the **New input** blade, provide the following values.</span></span>

    <span data-ttu-id="35bb7-130">![Adición de una entrada al trabajo](./media/data-lake-store-stream-analytics/create.input.2.png "Adición de una entrada al trabajo")</span><span class="sxs-lookup"><span data-stu-id="35bb7-130">![Add an input to your job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input to your job")</span></span>

    * <span data-ttu-id="35bb7-131">En **Alias de entrada**, escriba un nombre único para la entrada del trabajo.</span><span class="sxs-lookup"><span data-stu-id="35bb7-131">For **Input alias**, enter a unique name for the job input.</span></span>
    * <span data-ttu-id="35bb7-132">En **Source type** (Tipo de origen), seleccione **Flujo de datos**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="35bb7-133">En **Origen**, seleccione **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="35bb7-134">En **Suscripción**, seleccione **Usar almacenamiento de blobs de la suscripción actual**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="35bb7-135">En **Cuenta de almacenamiento**, seleccione la cuenta de almacenamiento que creó como parte de los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="35bb7-135">For **Storage account**, select the storage account that you created as part of the prerequisites.</span></span> 
    * <span data-ttu-id="35bb7-136">En **Contenedor**, seleccione el contenedor que creó en la cuenta de almacenamiento seleccionada.</span><span class="sxs-lookup"><span data-stu-id="35bb7-136">For **Container**, select the container that you created in the selected storage account.</span></span>
    * <span data-ttu-id="35bb7-137">En **Formato de serialización de eventos**, seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="35bb7-138">En **Delimitador**, seleccione **tabulación**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="35bb7-139">En **Codificación**, seleccione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="35bb7-140">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-140">Click **Create**.</span></span> <span data-ttu-id="35bb7-141">El portal ahora agrega la entrada y prueba la conexión a ella.</span><span class="sxs-lookup"><span data-stu-id="35bb7-141">The portal now adds the input and tests the connection to it.</span></span>


## <a name="create-a-data-lake-store-output-for-the-job"></a><span data-ttu-id="35bb7-142">Creación de una salida del Almacén de Data Lake para el trabajo</span><span class="sxs-lookup"><span data-stu-id="35bb7-142">Create a Data Lake Store output for the job</span></span>

1. <span data-ttu-id="35bb7-143">Haga clic en la página del trabajo de Stream Analytics, haga clic en la pestaña **Outputs** (Salidas) y después haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-143">Open the page for the Stream Analytics job, click the **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="35bb7-144">![Adición de una salida al trabajo](./media/data-lake-store-stream-analytics/create.output.1.png "Adición de una salida al trabajo")</span><span class="sxs-lookup"><span data-stu-id="35bb7-144">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output to your job")</span></span>

2. <span data-ttu-id="35bb7-145">En la hoja **Nueva salida**, proporcione los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="35bb7-145">On the **New output** blade, provide the following values.</span></span>

    <span data-ttu-id="35bb7-146">![Adición de una salida al trabajo](./media/data-lake-store-stream-analytics/create.output.2.png "Adición de una salida al trabajo")</span><span class="sxs-lookup"><span data-stu-id="35bb7-146">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output to your job")</span></span>

    * <span data-ttu-id="35bb7-147">En **Alias de salida**, escriba un nombre único para la salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="35bb7-147">For **Output alias**, enter a a unique name for the job output.</span></span> <span data-ttu-id="35bb7-148">Se trata de un nombre descriptivo utilizado en las consultas para dirigir la salida de la consulta a este Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="35bb7-148">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span>
    * <span data-ttu-id="35bb7-149">En **Receptor**, seleccione **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="35bb7-150">Se le pedirá que autorice el acceso a la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35bb7-150">You will be prompted to authorize access to Data Lake Store account.</span></span> <span data-ttu-id="35bb7-151">Haga clic en **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="35bb7-152">En la hoja **Nueva salida**, proporcione los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="35bb7-152">On the **New output** blade, continue to provide the following values.</span></span>

    <span data-ttu-id="35bb7-153">![Adición de una salida al trabajo](./media/data-lake-store-stream-analytics/create.output.3.png "Adición de una salida al trabajo")</span><span class="sxs-lookup"><span data-stu-id="35bb7-153">![Add an output to your job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output to your job")</span></span>

    * <span data-ttu-id="35bb7-154">En **Account name** (Nombre de cuenta), seleccione la cuenta de Data Lake Store que ya ha creado como ubicación a la que quiere que se envíe la salida del trabajo.</span><span class="sxs-lookup"><span data-stu-id="35bb7-154">For **Account name**, select the Data Lake Store account you already created where you want the job output to be sent to.</span></span>
    * <span data-ttu-id="35bb7-155">En **Patrón de prefijo de la ruta**, escriba una ruta de archivo usada para escribir los archivos en la cuenta de Data Lake Store especificada.</span><span class="sxs-lookup"><span data-stu-id="35bb7-155">For **Path prefix pattern**, enter a file path used to write your files within the specified Data Lake Store account.</span></span>
    * <span data-ttu-id="35bb7-156">En **Date format** (Formato de fecha), si usó un token de fecha en la ruta del prefijo, puede seleccionar el formato de fecha en el que se organizan sus archivos.</span><span class="sxs-lookup"><span data-stu-id="35bb7-156">For **Date format**, if you used a date token in the prefix path, you can select the date format in which your files are organized.</span></span>
    * <span data-ttu-id="35bb7-157">En **Time format** (Formato de hora), si usó un token de hora en la ruta del prefijo, especifique el formato de hora en el que se organizan sus archivos.</span><span class="sxs-lookup"><span data-stu-id="35bb7-157">For **Time format**, if you used a time token in the prefix path, specify the time format in which your files are organized.</span></span>
    * <span data-ttu-id="35bb7-158">En **Formato de serialización de eventos**, seleccione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="35bb7-159">En **Delimitador**, seleccione **tabulación**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="35bb7-160">En **Codificación**, seleccione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="35bb7-161">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-161">Click **Create**.</span></span> <span data-ttu-id="35bb7-162">El portal ahora agrega la salida y prueba la conexión a ella.</span><span class="sxs-lookup"><span data-stu-id="35bb7-162">The portal now adds the output and tests the connection to it.</span></span>
    
## <a name="run-the-stream-analytics-job"></a><span data-ttu-id="35bb7-163">Ejecución del trabajo de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="35bb7-163">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="35bb7-164">Para ejecutar un trabajo de Stream Analytics, debe ejecutar una consulta desde la pestaña **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-164">To run a Stream Analytics job, you must run a query from the **Query** tab.</span></span> <span data-ttu-id="35bb7-165">En este tutorial, puede ejecutar la consulta de ejemplo mediante el reemplazo de los marcadores de posición con los alias de entrada y salida del trabajo, tal como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="35bb7-165">For this tutorial, you can run the sample query by replacing the placeholders with the job input and output aliases, as shown in the screen capture below.</span></span>

    <span data-ttu-id="35bb7-166">![Ejecución de una consulta](./media/data-lake-store-stream-analytics/run.query.png "Ejecución de una consulta")</span><span class="sxs-lookup"><span data-stu-id="35bb7-166">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="35bb7-167">Haga clic en **Guardar** en la parte superior de la pantalla y, a continuación, en **Overview** (Introducción), haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-167">Click **Save** from the top of the screen, and then from the **Overview** tab, click **Start**.</span></span> <span data-ttu-id="35bb7-168">En el cuadro de diálogo, seleccione **Hora personalizada** y, después, seleccione la fecha y la hora actuales.</span><span class="sxs-lookup"><span data-stu-id="35bb7-168">From the dialog box, select **Custom Time**, and then set the current date and time.</span></span>

    <span data-ttu-id="35bb7-169">![Establecimiento de la hora del trabajo](./media/data-lake-store-stream-analytics/run.query.2.png "Establecimiento de la hora del trabajo")</span><span class="sxs-lookup"><span data-stu-id="35bb7-169">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="35bb7-170">Haga clic en **Iniciar** para iniciar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="35bb7-170">Click **Start** to start the job.</span></span> <span data-ttu-id="35bb7-171">Puede tardar unos minutos en iniciarse el trabajo.</span><span class="sxs-lookup"><span data-stu-id="35bb7-171">It can take up to a couple minutes to start the job.</span></span>

3. <span data-ttu-id="35bb7-172">Para desencadenar el trabajo que selecciona los datos del blob, copie un archivo de datos de ejemplo en el contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="35bb7-172">To trigger the job to pick the data from the blob, copy a sample data file to the blob container.</span></span> <span data-ttu-id="35bb7-173">Puede obtener un archivo de datos de ejemplo en el [repositorio Git de Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="35bb7-173">You can get a sample data file from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="35bb7-174">En este tutorial, vamos a copiar el archivo **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="35bb7-174">For this tutorial, let's copy the file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="35bb7-175">Puede utilizar varios clientes, como el [explorador de Almacenamiento de Azure](http://storageexplorer.com/), para cargar datos en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="35bb7-175">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), to upload data to a blob container.</span></span>

4. <span data-ttu-id="35bb7-176">En la pestaña **Overview** (Introducción), en **Monitoring** (Supervisión), consulte cómo se han procesado los datos.</span><span class="sxs-lookup"><span data-stu-id="35bb7-176">From the **Overview** tab, under **Monitoring**, see how the data was processed.</span></span>

    <span data-ttu-id="35bb7-177">![Supervisión de trabajos](./media/data-lake-store-stream-analytics/run.query.3.png "Supervisión de trabajos")</span><span class="sxs-lookup"><span data-stu-id="35bb7-177">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="35bb7-178">Finalmente, puede comprobar que los datos de salida del trabajo están disponibles en la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="35bb7-178">Finally, you can verify that the job output data is available in the Data Lake Store account.</span></span> 

    <span data-ttu-id="35bb7-179">![Comprobación de la salida](./media/data-lake-store-stream-analytics/run.query.4.png "Comprobación de la salida")</span><span class="sxs-lookup"><span data-stu-id="35bb7-179">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="35bb7-180">En el panel del Explorador de datos, tenga en cuenta que la salida se escribe en una ruta de carpeta, según lo especificado en la configuración de salida de Data Lake Store (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="35bb7-180">In the Data Explorer pane, notice that the output is written to a folder path as specified in the Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="35bb7-181">Consulte también</span><span class="sxs-lookup"><span data-stu-id="35bb7-181">See also</span></span>
* [<span data-ttu-id="35bb7-182">Creación de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="35bb7-182">Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
