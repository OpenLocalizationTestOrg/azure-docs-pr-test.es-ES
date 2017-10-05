---
title: "Invocación de programas Spark desde Azure Data Factory | Microsoft Docs"
description: "Obtenga información sobre cómo invocar programas Spark desde Data Factory de Azure mediante la actividad MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="5125e-103">Invocación de programas Spark desde canalizaciones de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5125e-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5125e-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="5125e-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="5125e-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="5125e-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5125e-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="5125e-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5125e-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="5125e-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5125e-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="5125e-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5125e-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5125e-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5125e-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5125e-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5125e-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="5125e-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5125e-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5125e-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5125e-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="5125e-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="5125e-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="5125e-114">Introduction</span></span>
<span data-ttu-id="5125e-115">La actividad de Spark es una de las [actividades de transformación de datos](data-factory-data-transformation-activities.md) compatibles con Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5125e-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="5125e-116">Esta actividad ejecuta el programa Spark especificado en el clúster de Apache Spark en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5125e-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="5125e-117">La actividad de Spark no admite clústeres de HDInsight Spark que usan una instancia de Azure Data Lake Store como almacenamiento principal.</span><span class="sxs-lookup"><span data-stu-id="5125e-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="5125e-118">La actividad de Spark admite solo los clústeres de HDInsight Spark existentes (los suyos propios).</span><span class="sxs-lookup"><span data-stu-id="5125e-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="5125e-119">No admite un servicio vinculado de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="5125e-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="5125e-120">Tutorial: creación de una canalización con actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="5125e-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="5125e-121">Estos son los pasos habituales para crear una canalización de Data Factory con una actividad de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="5125e-122">Creación de una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-122">Create a data factory.</span></span>
2. <span data-ttu-id="5125e-123">Cree un servicio vinculado de Azure Storage para vincular la instancia de Azure Storage asociada con el clúster de HDInsight Spark a la instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5125e-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="5125e-124">Cree un servicio vinculado de Azure HDInsight para vincular el clúster de Apache Spark en Azure HDInsight con la instancia de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5125e-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="5125e-125">Cree un conjunto de datos que haga referencia al servicio vinculado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5125e-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="5125e-126">Actualmente, debe especificar un conjunto de datos de salida para una actividad incluso si no se produce ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="5125e-127">Cree una canalización con la actividad de Spark que haga referencia al servicio vinculado de HDInsight creado en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="5125e-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="5125e-128">La actividad se configura con el conjunto de datos que creó en el paso anterior como un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="5125e-129">El conjunto de datos de salida es lo que impulsa la programación (cada hora, cada día, etc.).</span><span class="sxs-lookup"><span data-stu-id="5125e-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="5125e-130">Por lo tanto, debe especificar el conjunto de datos de salida aunque la actividad no produzca realmente una salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5125e-131">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5125e-131">Prerequisites</span></span>
1. <span data-ttu-id="5125e-132">Cree una **cuenta de Azure Storage de uso general** siguiendo las instrucciones del tutorial: [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5125e-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="5125e-133">Cree un **clúster de Apache Spark en Azure HDInsight** siguiendo las instrucciones del tutorial: [Creación de un clúster de Apache Spark en Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5125e-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="5125e-134">Asocie la cuenta de Azure Storage creada en el paso 1 con este clúster.</span><span class="sxs-lookup"><span data-stu-id="5125e-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="5125e-135">Descargue y revise el archivo de script de Python **test.py** ubicado en: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="5125e-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="5125e-136">Cargue **test.py** en la carpeta **pyFiles** del contenedor **adfspark** de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="5125e-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="5125e-137">Cree el contenedor y la carpeta si no existen.</span><span class="sxs-lookup"><span data-stu-id="5125e-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="5125e-138">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="5125e-138">Create data factory</span></span>
<span data-ttu-id="5125e-139">Comencemos con la creación de la factoría de datos en este paso.</span><span class="sxs-lookup"><span data-stu-id="5125e-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="5125e-140">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5125e-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5125e-141">En el menú de la izquierda, haga clic en **NUEVO**, en **Datos y Análisis** y en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="5125e-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="5125e-142">En la hoja **Nueva factoría de datos**, escriba **SparkDF** para el nombre.</span><span class="sxs-lookup"><span data-stu-id="5125e-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5125e-143">El nombre de Azure Data Factory debe ser **único de forma global**.</span><span class="sxs-lookup"><span data-stu-id="5125e-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="5125e-144">Si aparece el error: **El nombre "SparkDF" de factoría de datos no está disponible**.</span><span class="sxs-lookup"><span data-stu-id="5125e-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="5125e-145">Cambie el nombre de la factoría de datos (por ejemplo, suNombreSparkDFdate) e intente crearla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="5125e-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="5125e-146">Consulte el tema [Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para conocer las reglas de nomenclatura para los artefactos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5125e-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="5125e-147">Seleccione la **suscripción de Azure** donde desea crear la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="5125e-148">Seleccione un **grupo de recursos** de Azure existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="5125e-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="5125e-149">Seleccione la opción **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="5125e-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="5125e-150">Haga clic en **Crear** en la hoja **Nueva fábrica de datos**.</span><span class="sxs-lookup"><span data-stu-id="5125e-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5125e-151">Para crear instancias de Data Factory, es preciso ser miembro del rol [Colaborador de Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) en el nivel de grupo de recursos o suscripción.</span><span class="sxs-lookup"><span data-stu-id="5125e-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="5125e-152">Se ve que la factoría de datos se crea en el **panel** de Azure Portal de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="5125e-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="5125e-153">Tras crear correctamente la factoría de datos, se ve la página de la factoría de datos, que muestra el contenido de la misma.</span><span class="sxs-lookup"><span data-stu-id="5125e-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="5125e-154">Si no ve la página de la factoría de datos, haga clic en el icono de la factoría de datos en el panel.</span><span class="sxs-lookup"><span data-stu-id="5125e-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Hoja de la Factoría de datos](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="5125e-156">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="5125e-156">Create linked services</span></span>
<span data-ttu-id="5125e-157">En este paso, creará dos servicios vinculados, uno para vincular el clúster de Spark a la factoría de datos y el otro para vincular la instancia de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="5125e-158">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="5125e-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="5125e-159">En este paso, vinculará su cuenta de Almacenamiento de Azure con su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="5125e-160">Un conjunto de datos creado en un paso más adelante en este tutorial hace referencia a este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="5125e-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="5125e-161">El servicio vinculado de HDInsight que se define en el paso siguiente también hace referencia a este servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="5125e-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="5125e-162">Haga clic en **Crear e implementar** en la hoja **Data Factory** de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="5125e-163">Esto inicia el Editor de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5125e-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="5125e-164">Haga clic en **Nuevo almacén de datos** y elija **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="5125e-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nuevo almacén de datos - Azure Storage - menú](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="5125e-166">Debería ver el **script JSON** para crear un servicio vinculado de Azure Storage en el editor.</span><span class="sxs-lookup"><span data-stu-id="5125e-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Servicio vinculado de Almacenamiento de Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="5125e-168">Reemplace **nombre de cuenta** y **clave de cuenta** con el nombre y la clave de acceso de la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5125e-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="5125e-169">Para aprender a obtener la clave de acceso de almacenamiento, consulte la información sobre cómo ver, copiar y regenerar las claves de acceso de almacenamiento en [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5125e-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="5125e-170">Para implementar el servicio vinculado, haga clic en **Implementar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="5125e-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="5125e-171">Una vez que el servicio vinculado se ha implementado correctamente, la ventana **Draft-1** (Borrador 1) debería desaparecer y, en la vista de árbol de la izquierda, debería aparecer **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5125e-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="5125e-172">Creación del servicio vinculado de HDInsight</span><span class="sxs-lookup"><span data-stu-id="5125e-172">Create HDInsight linked service</span></span>
<span data-ttu-id="5125e-173">En este paso, se crea un servicio vinculado de Azure HDInsight para vincular el clúster de Apache Spark con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="5125e-174">El clúster de HDInsight se usa para ejecutar el programa Spark especificado en la actividad de Spark de la canalización en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5125e-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="5125e-175">Haga clic en **... Más** en la barra de herramientas, haga clic en **Nuevo proceso** y después haga clic en **Clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5125e-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Creación del servicio vinculado de HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="5125e-177">Copie y pegue el fragmento de código siguiente en la ventana **Borrador 1** .</span><span class="sxs-lookup"><span data-stu-id="5125e-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="5125e-178">En el Editor de JSON, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="5125e-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="5125e-179">Especifique el identificador **URI** del clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="5125e-180">Por ejemplo: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="5125e-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="5125e-181">Especifique el nombre del **usuario** que tiene acceso al clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="5125e-182">Especifique la **contraseña** para el usuario.</span><span class="sxs-lookup"><span data-stu-id="5125e-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="5125e-183">Especifique el **servicio vinculado de Azure Storage** asociado con el clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="5125e-184">En este ejemplo, es: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5125e-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="5125e-185">La actividad de Spark no admite clústeres de HDInsight Spark que usan una instancia de Azure Data Lake Store como almacenamiento principal.</span><span class="sxs-lookup"><span data-stu-id="5125e-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="5125e-186">La actividad de Spark admite solo el clúster de HDInsight Spark existente (el suyo propio).</span><span class="sxs-lookup"><span data-stu-id="5125e-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="5125e-187">No admite un servicio vinculado de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="5125e-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="5125e-188">Vea [Servicio vinculado de HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obtener más información sobre el servicio vinculado de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5125e-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="5125e-189">Para implementar el servicio vinculado, haga clic en **Implementar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="5125e-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="5125e-190">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="5125e-190">Create output dataset</span></span>
<span data-ttu-id="5125e-191">El conjunto de datos de salida es lo que impulsa la programación (cada hora, cada día, etc.).</span><span class="sxs-lookup"><span data-stu-id="5125e-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="5125e-192">Por lo tanto, debe especificar el conjunto de datos de salida para la actividad de Spark en la canalización aunque la actividad no produzca realmente una salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="5125e-193">Es opcional especificar un conjunto de datos de entrada para la actividad.</span><span class="sxs-lookup"><span data-stu-id="5125e-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="5125e-194">En el **Editor de Data Factory**, haga clic en **... Más** en la barra de comandos y luego en **Nuevo conjunto de datos**; después, seleccione **Almacenamiento de blobs de Azure**.</span><span class="sxs-lookup"><span data-stu-id="5125e-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="5125e-195">Copie y pegue el fragmento de código siguiente en la ventana Borrador-1.</span><span class="sxs-lookup"><span data-stu-id="5125e-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="5125e-196">El fragmento de código JSON define un conjunto de datos denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="5125e-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="5125e-197">Además, especifica que los resultados se almacenan en el contenedor de blobs llamado **adfspark** y en la carpeta llamada **pyFiles/output**.</span><span class="sxs-lookup"><span data-stu-id="5125e-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="5125e-198">Como se mencionó anteriormente, este conjunto de datos es un conjunto de datos ficticio.</span><span class="sxs-lookup"><span data-stu-id="5125e-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="5125e-199">El programa Spark de este ejemplo no genera ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="5125e-200">La sección **availability** especifica que el conjunto de datos de salida se genera diariamente.</span><span class="sxs-lookup"><span data-stu-id="5125e-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="5125e-201">Para implementar el conjunto de datos, haga clic en **Implementar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="5125e-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="5125e-202">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="5125e-202">Create pipeline</span></span>
<span data-ttu-id="5125e-203">En este paso, crea una canalización con una actividad de **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="5125e-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="5125e-204">Actualmente, el conjunto de datos de salida es lo que controla la programación, por lo que debe crear un conjunto de datos de salida aunque la actividad no genere ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="5125e-205">Si la actividad no toma ninguna entrada, puede omitir la creación del conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="5125e-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="5125e-206">Por lo tanto, no se especifica ningún conjunto de datos de entrada en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5125e-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="5125e-207">En **Data Factory Editor**, haga clic en **… Más** en la barra de comandos y después haga clic en **Nueva canalización**.</span><span class="sxs-lookup"><span data-stu-id="5125e-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="5125e-208">Reemplace el script en la ventana Draft-1 con el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="5125e-208">Replace the script in the Draft-1 window with the following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="5125e-209">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="5125e-209">Note the following points:</span></span>
    - <span data-ttu-id="5125e-210">La propiedad de **tipo** se establece en **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="5125e-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="5125e-211">El valor de **rootPath** se establece en **adfspark\\pyFiles**, donde adfspark es el contenedor de Azure Blob y pyFiles es la carpeta adecuada en ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="5125e-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="5125e-212">En este ejemplo, la instancia de Azure Blob Storage es la que está asociada con el clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="5125e-213">Puede cargar el archivo en un almacenamiento de Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="5125e-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="5125e-214">Si lo hace, cree un servicio vinculado de Azure Storage para vincular esa cuenta de almacenamiento con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="5125e-215">A continuación, especifique el nombre del servicio vinculado como un valor de la propiedad **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5125e-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="5125e-216">Consulte las [propiedades de la actividad de Spark](#spark-activity-properties) para más detalles sobre esta y otras propiedades que admite la actividad de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="5125e-217">El valor de **entryFilePath** se establece en **test.py**, que es el archivo de Python.</span><span class="sxs-lookup"><span data-stu-id="5125e-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="5125e-218">La propiedad **getDebugInfo** está establecida en **Siempre**, lo que significa que siempre se generan archivos de registro (acierto o error).</span><span class="sxs-lookup"><span data-stu-id="5125e-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="5125e-219">Se recomienda que no establezca esta propiedad como `Always` en un entorno de producción, a menos que esté solucionando un problema.</span><span class="sxs-lookup"><span data-stu-id="5125e-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="5125e-220">La sección de **salida** tiene un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="5125e-221">Debe especificar un conjunto de datos de salida, incluso si el programa de Spark no genera ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="5125e-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="5125e-222">El conjunto de datos de salida impulsa la programación de la canalización (cada hora, cada día, etc.).</span><span class="sxs-lookup"><span data-stu-id="5125e-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="5125e-223">Para obtener información detallada sobre las propiedades que la actividad de Spark admite, vea [Propiedades de la actividad de Spark](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5125e-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="5125e-224">Haga clic en **Implementar** en la barra de comandos para implementar la canalización.</span><span class="sxs-lookup"><span data-stu-id="5125e-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="5125e-225">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="5125e-225">Monitor pipeline</span></span>
1. <span data-ttu-id="5125e-226">Haga clic en el botón **X** para cerrar las hojas de Data Factory Editor y volver a página principal de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5125e-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="5125e-227">Haga clic en **Supervisión y administración** para iniciar la aplicación de supervisión en otra pestaña.</span><span class="sxs-lookup"><span data-stu-id="5125e-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![Icono Supervisión y administración](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="5125e-229">Cambie el filtro **Hora de inicio** en la parte superior por **2/1/2017** y haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5125e-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="5125e-230">Debería ver solo una ventana de actividad, ya que solo hay un día entre las horas de inicio (2017-02-01) y fin (2017-02-02) de la canalización.</span><span class="sxs-lookup"><span data-stu-id="5125e-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="5125e-231">Confirme que el estado del segmento de datos es **Listo**.</span><span class="sxs-lookup"><span data-stu-id="5125e-231">Confirm that the data slice is in **ready** state.</span></span>

    ![Supervisar la canalización](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="5125e-233">Seleccione la **ventana actividad** para ver los detalles sobre la ejecución de la actividad.</span><span class="sxs-lookup"><span data-stu-id="5125e-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="5125e-234">Si se produce un error, puede ver detalles sobre él en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="5125e-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="5125e-235">Verificación de los resultados</span><span class="sxs-lookup"><span data-stu-id="5125e-235">Verify the results</span></span>

1. <span data-ttu-id="5125e-236">Inicie **Jupyter Notebook** para el clúster de HDInsight Spark; para ello, navegue a: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="5125e-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="5125e-237">También puede iniciar el panel del clúster de HDInsight Spark y después inicie **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="5125e-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="5125e-238">Haga clic en **Nuevo** -> **PySpark** para iniciar un nuevo cuaderno.</span><span class="sxs-lookup"><span data-stu-id="5125e-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Nuevo Jupyter Notebook](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="5125e-240">Ejecute el siguiente comando; para ello, copie y peque el texto y presione **MAYÚS + ENTRAR** al final de la segunda instrucción.</span><span class="sxs-lookup"><span data-stu-id="5125e-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="5125e-241">Confirme que ve los datos de la tabla hvac:</span><span class="sxs-lookup"><span data-stu-id="5125e-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Resultados de la consulta Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="5125e-243">Vea la sección [Ejecución de una consulta de Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) para obtener instrucciones detalladas.</span><span class="sxs-lookup"><span data-stu-id="5125e-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="5125e-244">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5125e-244">Troubleshooting</span></span>
<span data-ttu-id="5125e-245">Puesto que establece **getDebugInfo** en **Siempre**, aparece una subcarpeta de **registro** en la carpeta **pyFiles** del contenedor de Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="5125e-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="5125e-246">El archivo de registro en la carpeta de registro proporciona detalles adicionales.</span><span class="sxs-lookup"><span data-stu-id="5125e-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="5125e-247">Este archivo de registro es especialmente útil cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="5125e-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="5125e-248">En un entorno de producción, puede establecerlo en **Error**.</span><span class="sxs-lookup"><span data-stu-id="5125e-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="5125e-249">Para solucionar problemas, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5125e-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="5125e-250">Vaya a `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="5125e-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Aplicación de IU de YARN](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="5125e-252">Haga clic en **Registros** para uno de los intentos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="5125e-252">Click **Logs** for one of the run attempts.</span></span>

    ![Página de aplicación](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="5125e-254">Debería ver información adicional sobre el error en la página de registro.</span><span class="sxs-lookup"><span data-stu-id="5125e-254">You should see additional error information in the log page.</span></span>

    ![Error de registro](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="5125e-256">En las secciones siguientes se proporciona información sobre las entidades de Data Factory para usar un clúster de Apache Spark y una actividad de Spark en su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5125e-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="5125e-257">Propiedades de la actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="5125e-257">Spark activity properties</span></span>
<span data-ttu-id="5125e-258">Esta es la definición JSON de ejemplo de una canalización con la actividad de Spark:</span><span class="sxs-lookup"><span data-stu-id="5125e-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="5125e-259">En la siguiente tabla se describen las propiedades JSON que se usan en la definición de JSON:</span><span class="sxs-lookup"><span data-stu-id="5125e-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="5125e-260">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5125e-260">Property</span></span> | <span data-ttu-id="5125e-261">Descripción</span><span class="sxs-lookup"><span data-stu-id="5125e-261">Description</span></span> | <span data-ttu-id="5125e-262">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5125e-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="5125e-263">name</span><span class="sxs-lookup"><span data-stu-id="5125e-263">name</span></span> | <span data-ttu-id="5125e-264">Nombre de la actividad en la canalización.</span><span class="sxs-lookup"><span data-stu-id="5125e-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="5125e-265">Sí</span><span class="sxs-lookup"><span data-stu-id="5125e-265">Yes</span></span> |
| <span data-ttu-id="5125e-266">Descripción</span><span class="sxs-lookup"><span data-stu-id="5125e-266">description</span></span> | <span data-ttu-id="5125e-267">Texto que describe para qué se usa la actividad.</span><span class="sxs-lookup"><span data-stu-id="5125e-267">Text describing what the activity does.</span></span> | <span data-ttu-id="5125e-268">No</span><span class="sxs-lookup"><span data-stu-id="5125e-268">No</span></span> |
| <span data-ttu-id="5125e-269">type</span><span class="sxs-lookup"><span data-stu-id="5125e-269">type</span></span> | <span data-ttu-id="5125e-270">Esta propiedad debe establecerse en HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="5125e-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="5125e-271">Sí</span><span class="sxs-lookup"><span data-stu-id="5125e-271">Yes</span></span> |
| <span data-ttu-id="5125e-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5125e-272">linkedServiceName</span></span> | <span data-ttu-id="5125e-273">Nombre del servicio vinculado de HDInsight en el que se ejecuta el programa de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="5125e-274">Sí</span><span class="sxs-lookup"><span data-stu-id="5125e-274">Yes</span></span> |
| <span data-ttu-id="5125e-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="5125e-275">rootPath</span></span> | <span data-ttu-id="5125e-276">Contenedor de blobs de Azure y la carpeta que contiene el archivo de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="5125e-277">El nombre del archivo distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5125e-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="5125e-278">Sí</span><span class="sxs-lookup"><span data-stu-id="5125e-278">Yes</span></span> |
| <span data-ttu-id="5125e-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="5125e-279">entryFilePath</span></span> | <span data-ttu-id="5125e-280">Ruta de acceso relativa a la carpeta raíz del código o el paquete de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="5125e-281">Sí</span><span class="sxs-lookup"><span data-stu-id="5125e-281">Yes</span></span> |
| <span data-ttu-id="5125e-282">className</span><span class="sxs-lookup"><span data-stu-id="5125e-282">className</span></span> | <span data-ttu-id="5125e-283">Clase principal de Spark o Java de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5125e-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="5125e-284">No</span><span class="sxs-lookup"><span data-stu-id="5125e-284">No</span></span> |
| <span data-ttu-id="5125e-285">argumentos</span><span class="sxs-lookup"><span data-stu-id="5125e-285">arguments</span></span> | <span data-ttu-id="5125e-286">Lista de argumentos de línea de comandos del programa de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="5125e-287">No</span><span class="sxs-lookup"><span data-stu-id="5125e-287">No</span></span> |
| <span data-ttu-id="5125e-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="5125e-288">proxyUser</span></span> | <span data-ttu-id="5125e-289">Cuenta de usuario de suplantación para ejecutar el programa de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="5125e-290">No</span><span class="sxs-lookup"><span data-stu-id="5125e-290">No</span></span> |
| <span data-ttu-id="5125e-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="5125e-291">sparkConfig</span></span> | <span data-ttu-id="5125e-292">Especifique valores para propiedades de configuración de Spark indicados en el tema [Spark Configuration: Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties) (Configuración de Spark: Propiedades de aplicación).</span><span class="sxs-lookup"><span data-stu-id="5125e-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="5125e-293">No</span><span class="sxs-lookup"><span data-stu-id="5125e-293">No</span></span> |
| <span data-ttu-id="5125e-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="5125e-294">getDebugInfo</span></span> | <span data-ttu-id="5125e-295">Especifica si se copian los archivos de registro de Spark en el almacenamiento de Azure que usa el clúster de HDInsight que especifica sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="5125e-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="5125e-296">Valores permitidos: Ninguno, Siempre o Error.</span><span class="sxs-lookup"><span data-stu-id="5125e-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="5125e-297">Valor predeterminado: Ninguno.</span><span class="sxs-lookup"><span data-stu-id="5125e-297">Default value: None.</span></span> | <span data-ttu-id="5125e-298">No</span><span class="sxs-lookup"><span data-stu-id="5125e-298">No</span></span> |
| <span data-ttu-id="5125e-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="5125e-299">sparkJobLinkedService</span></span> | <span data-ttu-id="5125e-300">El servicio vinculado de Azure Storage que contiene los registros, las dependencias y los archivos de trabajos de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="5125e-301">Si no especifica un valor para esta propiedad, se usa el almacenamiento asociado con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5125e-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="5125e-302">No</span><span class="sxs-lookup"><span data-stu-id="5125e-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="5125e-303">Estructura de carpetas</span><span class="sxs-lookup"><span data-stu-id="5125e-303">Folder structure</span></span>
<span data-ttu-id="5125e-304">La actividad de Spark no es compatible con un script en línea, al contrario que las actividades de Pig y Hive.</span><span class="sxs-lookup"><span data-stu-id="5125e-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="5125e-305">Los trabajos de Spark también son más ampliable que los de Pig y Hive.</span><span class="sxs-lookup"><span data-stu-id="5125e-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="5125e-306">En los trabajos de Spark, puede proporcionar varias dependencias como paquetes JAR (ubicados en la CLASSPATH de Java), archivos de Python (ubicados en la ruta PYTHONPATH) y cualquier otro archivo.</span><span class="sxs-lookup"><span data-stu-id="5125e-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="5125e-307">Cree la siguiente estructura de carpetas en la instancia de Azure Blob Storage a la que hace referencia el servicio vinculado de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5125e-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="5125e-308">Luego, cargue los archivos dependientes en las subcarpetas adecuadas de la carpeta raíz que representa **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="5125e-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="5125e-309">Por ejemplo, cargue los archivos de Python en la subcarpeta pyFiles y los archivos JAR en la subcarpeta jars de la carpeta raíz.</span><span class="sxs-lookup"><span data-stu-id="5125e-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="5125e-310">En el entorno de tiempo de ejecución, el servicio Data Factory espera la siguiente estructura de carpetas en Azure Blob Storage:</span><span class="sxs-lookup"><span data-stu-id="5125e-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="5125e-311">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="5125e-311">Path</span></span> | <span data-ttu-id="5125e-312">Descripción</span><span class="sxs-lookup"><span data-stu-id="5125e-312">Description</span></span> | <span data-ttu-id="5125e-313">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5125e-313">Required</span></span> | <span data-ttu-id="5125e-314">Escriba</span><span class="sxs-lookup"><span data-stu-id="5125e-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="5125e-315">.</span><span class="sxs-lookup"><span data-stu-id="5125e-315">.</span></span> | <span data-ttu-id="5125e-316">Ruta de acceso raíz del trabajo de Spark en el servicio vinculado de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5125e-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="5125e-317">Sí</span><span class="sxs-lookup"><span data-stu-id="5125e-317">Yes</span></span> | <span data-ttu-id="5125e-318">Carpeta</span><span class="sxs-lookup"><span data-stu-id="5125e-318">Folder</span></span> |
| <span data-ttu-id="5125e-319">&lt;Definida por el usuario&gt;</span><span class="sxs-lookup"><span data-stu-id="5125e-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="5125e-320">Ruta de acceso que apunta al archivo de entrada del trabajo de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="5125e-321">Sí</span><span class="sxs-lookup"><span data-stu-id="5125e-321">Yes</span></span> | <span data-ttu-id="5125e-322">Archivo</span><span class="sxs-lookup"><span data-stu-id="5125e-322">File</span></span> |
| <span data-ttu-id="5125e-323">./jars</span><span class="sxs-lookup"><span data-stu-id="5125e-323">./jars</span></span> | <span data-ttu-id="5125e-324">Todos los archivos de esta carpeta se cargan y se colocan en la ruta CLASSPATH de Java del clúster.</span><span class="sxs-lookup"><span data-stu-id="5125e-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="5125e-325">No</span><span class="sxs-lookup"><span data-stu-id="5125e-325">No</span></span> | <span data-ttu-id="5125e-326">Carpeta</span><span class="sxs-lookup"><span data-stu-id="5125e-326">Folder</span></span> |
| <span data-ttu-id="5125e-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="5125e-327">./pyFiles</span></span> | <span data-ttu-id="5125e-328">Todos los archivos de esta carpeta se cargan y se colocan en la ruta PYTHONPATH del clúster.</span><span class="sxs-lookup"><span data-stu-id="5125e-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="5125e-329">No</span><span class="sxs-lookup"><span data-stu-id="5125e-329">No</span></span> | <span data-ttu-id="5125e-330">Carpeta</span><span class="sxs-lookup"><span data-stu-id="5125e-330">Folder</span></span> |
| <span data-ttu-id="5125e-331">./files</span><span class="sxs-lookup"><span data-stu-id="5125e-331">./files</span></span> | <span data-ttu-id="5125e-332">Todos los archivos de esta carpeta se cargan y se colocan en el directorio de trabajo del ejecutor.</span><span class="sxs-lookup"><span data-stu-id="5125e-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="5125e-333">No</span><span class="sxs-lookup"><span data-stu-id="5125e-333">No</span></span> | <span data-ttu-id="5125e-334">Carpeta</span><span class="sxs-lookup"><span data-stu-id="5125e-334">Folder</span></span> |
| <span data-ttu-id="5125e-335">./archives</span><span class="sxs-lookup"><span data-stu-id="5125e-335">./archives</span></span> | <span data-ttu-id="5125e-336">Todos los archivos de esta carpeta están sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="5125e-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="5125e-337">No</span><span class="sxs-lookup"><span data-stu-id="5125e-337">No</span></span> | <span data-ttu-id="5125e-338">Carpeta</span><span class="sxs-lookup"><span data-stu-id="5125e-338">Folder</span></span> |
| <span data-ttu-id="5125e-339">./logs</span><span class="sxs-lookup"><span data-stu-id="5125e-339">./logs</span></span> | <span data-ttu-id="5125e-340">Carpeta donde se almacenan los registros del clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="5125e-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="5125e-341">No</span><span class="sxs-lookup"><span data-stu-id="5125e-341">No</span></span> | <span data-ttu-id="5125e-342">Carpeta</span><span class="sxs-lookup"><span data-stu-id="5125e-342">Folder</span></span> |

<span data-ttu-id="5125e-343">Este es un ejemplo de un almacenamiento que contiene dos archivos de trabajos de Spark en la instancia de Azure Blob Storage a la que hace referencia el servicio vinculado de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5125e-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
