---
title: aaaInvoke Spark programas de Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo programas de Spark tooinvoke desde una factoría de datos de Azure con Hola actividad MapReduce."
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
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="87531-103">Invocación de programas Spark desde canalizaciones de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="87531-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="87531-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="87531-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="87531-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="87531-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="87531-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="87531-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="87531-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="87531-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="87531-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="87531-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="87531-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="87531-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="87531-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="87531-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="87531-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="87531-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="87531-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="87531-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="87531-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="87531-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="87531-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="87531-114">Introduction</span></span>
<span data-ttu-id="87531-115">Actividad de Spark es uno de hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) compatible con Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="87531-116">Esta actividad ejecuta Hola especificado programa Spark en el clúster de Apache Spark en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="87531-117">La actividad de Spark no admite clústeres de HDInsight Spark que usan una instancia de Azure Data Lake Store como almacenamiento principal.</span><span class="sxs-lookup"><span data-stu-id="87531-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="87531-118">La actividad de Spark admite solo los clústeres de HDInsight Spark existentes (los suyos propios).</span><span class="sxs-lookup"><span data-stu-id="87531-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="87531-119">No admite un servicio vinculado de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="87531-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="87531-120">Tutorial: creación de una canalización con actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="87531-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="87531-121">Estos son los pasos típicos de hello toocreate una canalización de factoría de datos con una actividad de Spark.</span><span class="sxs-lookup"><span data-stu-id="87531-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="87531-122">Creación de una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="87531-122">Create a data factory.</span></span>
2. <span data-ttu-id="87531-123">Crear un toolink de servicio vinculado de almacenamiento de Azure en el almacenamiento de Azure que está asociado a la factoría de datos de toohello de clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="87531-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="87531-124">Crear un toolink de servicio vinculado de HDInsight de Azure su clúster Spark Apache de factoría de datos de toohello de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="87531-125">Crear un conjunto de datos que hace referencia el servicio de almacenamiento de Azure vinculada de toohello.</span><span class="sxs-lookup"><span data-stu-id="87531-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="87531-126">Actualmente, debe especificar un conjunto de datos de salida para una actividad incluso si no se produce ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="87531-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="87531-127">Crear una canalización con la actividad de Spark que hace referencia el servicio vinculado de HDInsight de toohello creado en #2.</span><span class="sxs-lookup"><span data-stu-id="87531-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="87531-128">actividad Hello se configura con el conjunto de datos de Hola que creó en el paso anterior de Hola como un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="87531-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="87531-129">conjunto de datos de salida de Hello es qué unidades Hola programación (etcetera diariamente, cada hora,.).</span><span class="sxs-lookup"><span data-stu-id="87531-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="87531-130">Por lo tanto, debe especificar el conjunto de datos de salida de hello aunque actividad hello no produce realmente un resultado.</span><span class="sxs-lookup"><span data-stu-id="87531-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="87531-131">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="87531-131">Prerequisites</span></span>
1. <span data-ttu-id="87531-132">Crear un **cuenta de almacenamiento de Azure para fines generales** siguiendo las instrucciones de tutorial de hello: [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="87531-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="87531-133">Crear un **clúster Apache Spark en HDInsight de Azure** siguiendo las instrucciones de tutorial de hello: [clúster crear Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="87531-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="87531-134">Asociar la cuenta de almacenamiento de Azure Hola que creó en el paso 1 de # con este clúster.</span><span class="sxs-lookup"><span data-stu-id="87531-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="87531-135">Descargue y revise el archivo de script de python de hello **test.py** situado en: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="87531-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="87531-136">Cargar **test.py** toohello **pyFiles** carpeta Hola **adfspark** contenedor en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="87531-137">Crear contenedor de Hola y la carpeta de hello si no existen.</span><span class="sxs-lookup"><span data-stu-id="87531-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="87531-138">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="87531-138">Create data factory</span></span>
<span data-ttu-id="87531-139">Puede empezar con la creación de factoría de datos de hello en este paso.</span><span class="sxs-lookup"><span data-stu-id="87531-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="87531-140">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="87531-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="87531-141">Haga clic en **NEW** en el menú de la izquierda hello, haga clic en **datos + análisis**y haga clic en **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="87531-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="87531-142">Hola **factoría de datos** hoja, escriba **SparkDF** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="87531-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="87531-143">nombre de Hola Hola Azure factoría de datos debe ser **único global**.</span><span class="sxs-lookup"><span data-stu-id="87531-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="87531-144">Si ve el error de hello: **nombre de generador de datos "SparkDF" no está disponible**.</span><span class="sxs-lookup"><span data-stu-id="87531-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="87531-145">Cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameSparkDFdate y pruebe a crear de nuevo.</span><span class="sxs-lookup"><span data-stu-id="87531-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="87531-146">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="87531-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="87531-147">Seleccione hello **suscripción de Azure** donde desea Hola datos generador toobe creado.</span><span class="sxs-lookup"><span data-stu-id="87531-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="87531-148">Seleccione un **grupo de recursos** de Azure existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="87531-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="87531-149">Seleccione **toodashboard Pin** opción.</span><span class="sxs-lookup"><span data-stu-id="87531-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="87531-150">Haga clic en **crear** en hello **factoría de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="87531-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="87531-151">instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="87531-152">Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="87531-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="87531-153">Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="87531-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="87531-154">Si no ve la página de factoría de datos de hello, haga clic en icono de saludo de la factoría de datos en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Hoja de la Factoría de datos](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="87531-156">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="87531-156">Create linked services</span></span>
<span data-ttu-id="87531-157">En este paso, creará dos servicios vinculados, una toolink su factoría de datos de Spark clúster tooyour y Hola otro toolink su factoría de datos de almacenamiento de Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="87531-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="87531-158">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="87531-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="87531-159">En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="87531-160">Un conjunto de datos que cree en un paso más adelante en este tutorial hace referencia servicio toothis vinculado.</span><span class="sxs-lookup"><span data-stu-id="87531-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="87531-161">servicio vinculado de HDInsight que define en el paso siguiente Hola Hola hace referencia servicio toothis vinculado.</span><span class="sxs-lookup"><span data-stu-id="87531-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="87531-162">Haga clic en **autor e implementar** en hello **factoría de datos** hoja de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="87531-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="87531-163">Debería ver Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="87531-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="87531-164">Haga clic en **Nuevo almacén de datos** y elija **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="87531-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nuevo almacén de datos - Azure Storage - menú](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="87531-166">Debería ver Hola **script JSON** para crear un almacenamiento de Azure de servicio en el editor de hello vinculado.</span><span class="sxs-lookup"><span data-stu-id="87531-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Servicio vinculado de Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="87531-168">Reemplace **nombre-cuenta** y **clave de cuenta** con la clave de acceso y nombre de hello de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="87531-169">toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="87531-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="87531-170">toodeploy Hola servicio vinculado, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="87531-171">Después de hello servicio vinculado se ha implementado correctamente, Hola **Draft-1** ventana debería desaparecer y verá **AzureStorageLinkedService** en vista de árbol de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="87531-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="87531-172">Creación del servicio vinculado de HDInsight</span><span class="sxs-lookup"><span data-stu-id="87531-172">Create HDInsight linked service</span></span>
<span data-ttu-id="87531-173">En este paso, creará toolink de servicio vinculado de HDInsight de Azure la factoría de datos de toohello de clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="87531-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="87531-174">clúster de HDInsight de Hello es programa de Spark de hello toorun utilizado especificado en la actividad de Spark hello de canalización de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="87531-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="87531-175">Haga clic en **... Más** en la barra de herramientas de hello, haga clic en **nuevo proceso**y, a continuación, haga clic en **clúster de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="87531-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Creación del servicio vinculado de HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="87531-177">Copie y pegue Hola siguiente fragmento de código toohello **Draft-1** ventana.</span><span class="sxs-lookup"><span data-stu-id="87531-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="87531-178">En el editor de JSON de hello, Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="87531-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="87531-179">Especificar hello **URI** para hello HDInsight Spark del clúster.</span><span class="sxs-lookup"><span data-stu-id="87531-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="87531-180">Por ejemplo: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="87531-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="87531-181">Especificar nombre de Hola de hello **usuario** quién tiene clúster de Spark toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="87531-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="87531-182">Especificar hello **contraseña** para el usuario.</span><span class="sxs-lookup"><span data-stu-id="87531-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="87531-183">Especificar hello **servicio vinculado de almacenamiento de Azure** que está asociado con el clúster de HDInsight Spark hello.</span><span class="sxs-lookup"><span data-stu-id="87531-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="87531-184">En este ejemplo, es: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="87531-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="87531-185">La actividad de Spark no admite clústeres de HDInsight Spark que usan una instancia de Azure Data Lake Store como almacenamiento principal.</span><span class="sxs-lookup"><span data-stu-id="87531-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="87531-186">La actividad de Spark admite solo el clúster de HDInsight Spark existente (el suyo propio).</span><span class="sxs-lookup"><span data-stu-id="87531-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="87531-187">No admite un servicio vinculado de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="87531-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="87531-188">Vea [servicio vinculado de HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obtener más información acerca de hello HDInsight servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="87531-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="87531-189">toodeploy Hola servicio vinculado, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="87531-190">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="87531-190">Create output dataset</span></span>
<span data-ttu-id="87531-191">conjunto de datos de salida de Hello es qué unidades Hola programación (etcetera diariamente, cada hora,.).</span><span class="sxs-lookup"><span data-stu-id="87531-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="87531-192">Por lo tanto, debe especificar un conjunto de datos de salida para la actividad de spark hello en canalización Hola aunque actividad hello realmente no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="87531-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="87531-193">Especificar un conjunto de datos de entrada para la actividad de hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="87531-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="87531-194">Hola **Editor de generador de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y seleccione **almacenamiento de blobs de Azure**.</span><span class="sxs-lookup"><span data-stu-id="87531-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="87531-195">Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="87531-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="87531-196">el fragmento de código de Hello JSON define un conjunto de datos denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="87531-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="87531-197">Además, se especifica que los resultados de Hola se almacenen en contenedor de blob de hello denominado **adfspark** y carpeta Hola llamada **pyFiles/salida**.</span><span class="sxs-lookup"><span data-stu-id="87531-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="87531-198">Como se mencionó anteriormente, este conjunto de datos es un conjunto de datos ficticio.</span><span class="sxs-lookup"><span data-stu-id="87531-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="87531-199">programa de Spark Hello en este ejemplo no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="87531-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="87531-200">Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se generen diariamente.</span><span class="sxs-lookup"><span data-stu-id="87531-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="87531-201">toodeploy Hola conjunto de datos, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="87531-202">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="87531-202">Create pipeline</span></span>
<span data-ttu-id="87531-203">En este paso, crea una canalización con una actividad de **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="87531-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="87531-204">Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="87531-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="87531-205">Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada.</span><span class="sxs-lookup"><span data-stu-id="87531-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="87531-206">Por lo tanto, no se especifica ningún conjunto de datos de entrada en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="87531-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="87531-207">Hola **Editor de generador de datos**, haga clic en **... Más** en Hola barra de comandos y, a continuación, haga clic en **nueva canalización**.</span><span class="sxs-lookup"><span data-stu-id="87531-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="87531-208">Reemplace el script de Hola en ventana hello Draft-1 con hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="87531-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

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
    <span data-ttu-id="87531-209">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="87531-209">Note hello following points:</span></span>
    - <span data-ttu-id="87531-210">Hola **tipo** propiedad se establece demasiado**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="87531-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="87531-211">Hola **Ruta_raíz** se establece demasiado**adfspark\\pyFiles** donde adfspark es contenedor de blobs de Azure de Hola y pyFiles es la carpeta correctamente en ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="87531-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="87531-212">En este ejemplo, hello almacenamiento de blobs de Azure es hello uno que esté asociado con el clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="87531-213">Puede cargar Hola archivo tooa almacenamiento de Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="87531-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="87531-214">Si lo hace, cree un toolink de servicio vinculado de almacenamiento de Azure que factoría de datos de toohello de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="87531-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="87531-215">A continuación, especificar nombre de Hola de servicio de hello vinculado como un valor de hello **sparkJobLinkedService** propiedad.</span><span class="sxs-lookup"><span data-stu-id="87531-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="87531-216">Vea [propiedades de la actividad de Spark](#spark-activity-properties) para obtener más información acerca de esta propiedad y otras propiedades compatibles con hello Spark actividad.</span><span class="sxs-lookup"><span data-stu-id="87531-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="87531-217">Hola **entryFilePath** se establece toohello **test.py**, que es el archivo de python de hello.</span><span class="sxs-lookup"><span data-stu-id="87531-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="87531-218">Hola **getDebugInfo** propiedad se establece demasiado**siempre**, lo que significa que los archivos de registro de hello siempre están generado (éxito o error).</span><span class="sxs-lookup"><span data-stu-id="87531-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="87531-219">Se recomienda que no establezca esta propiedad demasiado`Always` en un entorno de producción a menos que esté solucionando un problema.</span><span class="sxs-lookup"><span data-stu-id="87531-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="87531-220">Hola **genera** sección tiene un conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="87531-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="87531-221">Debe especificar un conjunto de datos de salida, incluso si el programa de spark hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="87531-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="87531-222">Hola salida dataset unidades Hola programación para canalización hello (etcetera diariamente, cada hora,.).</span><span class="sxs-lookup"><span data-stu-id="87531-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="87531-223">Para obtener más información sobre las propiedades de hello admitidas por las actividades de Spark, consulte [inspirará propiedades de la actividad](#spark-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="87531-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="87531-224">canalización de hello toodeploy, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="87531-225">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="87531-225">Monitor pipeline</span></span>
1. <span data-ttu-id="87531-226">Haga clic en **X** tooclose hojas de Editor de generador de datos y toonavigate página principal de toohello factoría de datos de nuevo.</span><span class="sxs-lookup"><span data-stu-id="87531-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="87531-227">Haga clic en **supervisar y administrar** hello toolaunch supervisión de la aplicación en otra ficha.</span><span class="sxs-lookup"><span data-stu-id="87531-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![Icono Supervisión y administración](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="87531-229">Hola de cambio **hora de inicio** filtrar en la parte superior de hello demasiado**2/1/2017**y haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="87531-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="87531-230">Debería ver sólo una ventana de actividad como hay solo un día entre hello (2017-02-01) de inicio y finalización (2017-02-02) de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="87531-231">Confirme que está ese segmento de datos de hello en **listo** estado.</span><span class="sxs-lookup"><span data-stu-id="87531-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Canalización de Hola de Monitor](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="87531-233">Seleccione hello **ventana actividad** toosee detalles acerca de la ejecución de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="87531-234">Si se produce un error, puede ver detalles sobre él en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="87531-235">Comprobar los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="87531-235">Verify hello results</span></span>

1. <span data-ttu-id="87531-236">Inicie **Jupyter Notebook** para el clúster de HDInsight Spark; para ello, navegue a: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="87531-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="87531-237">También puede iniciar el panel del clúster de HDInsight Spark y después inicie **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="87531-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="87531-238">Haga clic en **New** -> **PySpark** toostart un nuevo bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="87531-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Nuevo Jupyter Notebook](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="87531-240">Ejecución hello después del comando de copia y pegado de texto hello y presionando **MAYÚS + ENTRAR** final hello de la segunda instrucción de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="87531-241">Confirme que ve los datos de saludo de tabla de hvac Hola:</span><span class="sxs-lookup"><span data-stu-id="87531-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Resultados de la consulta Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="87531-243">Vea la sección [Ejecución de una consulta de Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) para obtener instrucciones detalladas.</span><span class="sxs-lookup"><span data-stu-id="87531-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="87531-244">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="87531-244">Troubleshooting</span></span>
<span data-ttu-id="87531-245">Puesto que establece **getDebugInfo** demasiado**siempre**, verá un **registro** subcarpeta en hello **pyFiles** carpeta en el contenedor de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="87531-246">archivo de registro de Hello en carpeta de registro de hello proporciona detalles adicionales.</span><span class="sxs-lookup"><span data-stu-id="87531-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="87531-247">Este archivo de registro es especialmente útil cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="87531-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="87531-248">En un entorno de producción, puede que desee tooset se demasiado**error**.</span><span class="sxs-lookup"><span data-stu-id="87531-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="87531-249">Para solucionar problemas, Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="87531-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="87531-250">Navegue demasiado`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="87531-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Aplicación de IU de YARN](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="87531-252">Haga clic en **registros** para uno de hello ejecutar intentos.</span><span class="sxs-lookup"><span data-stu-id="87531-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Página de aplicación](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="87531-254">Debería ver la información de error adicional en la página de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="87531-254">You should see additional error information in hello log page.</span></span>

    ![Error de registro](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="87531-256">Hello las secciones siguientes proporciona información sobre clústeres de Apache Spark de toouse de entidades de factoría de datos y la actividad de Spark en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="87531-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="87531-257">Propiedades de la actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="87531-257">Spark activity properties</span></span>
<span data-ttu-id="87531-258">Aquí está la definición de JSON de ejemplo de Hola de una canalización con Spark actividad:</span><span class="sxs-lookup"><span data-stu-id="87531-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="87531-259">Hello tabla siguiente describen propiedades JSON de hello utilizadas en hello definición JSON:</span><span class="sxs-lookup"><span data-stu-id="87531-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="87531-260">Propiedad</span><span class="sxs-lookup"><span data-stu-id="87531-260">Property</span></span> | <span data-ttu-id="87531-261">Descripción</span><span class="sxs-lookup"><span data-stu-id="87531-261">Description</span></span> | <span data-ttu-id="87531-262">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="87531-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="87531-263">name</span><span class="sxs-lookup"><span data-stu-id="87531-263">name</span></span> | <span data-ttu-id="87531-264">Nombre de actividad de hello en canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="87531-265">Sí</span><span class="sxs-lookup"><span data-stu-id="87531-265">Yes</span></span> |
| <span data-ttu-id="87531-266">description</span><span class="sxs-lookup"><span data-stu-id="87531-266">description</span></span> | <span data-ttu-id="87531-267">Texto que describe qué actividad hello hace.</span><span class="sxs-lookup"><span data-stu-id="87531-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="87531-268">No</span><span class="sxs-lookup"><span data-stu-id="87531-268">No</span></span> |
| <span data-ttu-id="87531-269">type</span><span class="sxs-lookup"><span data-stu-id="87531-269">type</span></span> | <span data-ttu-id="87531-270">Esta propiedad se debe establecer tooHDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="87531-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="87531-271">Sí</span><span class="sxs-lookup"><span data-stu-id="87531-271">Yes</span></span> |
| <span data-ttu-id="87531-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="87531-272">linkedServiceName</span></span> | <span data-ttu-id="87531-273">El nombre del programa Hola a HDInsight vinculados en qué Hola Spark se ejecuta el programa de servicio.</span><span class="sxs-lookup"><span data-stu-id="87531-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="87531-274">Sí</span><span class="sxs-lookup"><span data-stu-id="87531-274">Yes</span></span> |
| <span data-ttu-id="87531-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="87531-275">rootPath</span></span> | <span data-ttu-id="87531-276">contenedor de blobs de Azure de Hola y la carpeta que contiene el archivo de hello Spark.</span><span class="sxs-lookup"><span data-stu-id="87531-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="87531-277">nombre de archivo de Hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="87531-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="87531-278">Sí</span><span class="sxs-lookup"><span data-stu-id="87531-278">Yes</span></span> |
| <span data-ttu-id="87531-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="87531-279">entryFilePath</span></span> | <span data-ttu-id="87531-280">Carpeta de raíz de toohello de ruta de acceso relativa del programa Hola Spark/paquete de código.</span><span class="sxs-lookup"><span data-stu-id="87531-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="87531-281">Sí</span><span class="sxs-lookup"><span data-stu-id="87531-281">Yes</span></span> |
| <span data-ttu-id="87531-282">className</span><span class="sxs-lookup"><span data-stu-id="87531-282">className</span></span> | <span data-ttu-id="87531-283">Clase principal de Spark o Java de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="87531-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="87531-284">No</span><span class="sxs-lookup"><span data-stu-id="87531-284">No</span></span> |
| <span data-ttu-id="87531-285">argumentos</span><span class="sxs-lookup"><span data-stu-id="87531-285">arguments</span></span> | <span data-ttu-id="87531-286">Una lista de programas de Spark de toohello argumentos de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="87531-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="87531-287">No</span><span class="sxs-lookup"><span data-stu-id="87531-287">No</span></span> |
| <span data-ttu-id="87531-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="87531-288">proxyUser</span></span> | <span data-ttu-id="87531-289">programa de Spark hello tooexecute de tooimpersonate de la cuenta de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="87531-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="87531-290">No</span><span class="sxs-lookup"><span data-stu-id="87531-290">No</span></span> |
| <span data-ttu-id="87531-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="87531-291">sparkConfig</span></span> | <span data-ttu-id="87531-292">Especificar valores para propiedades de configuración de Spark enumerados en el tema de hello: [configuración Spark - propiedades de la aplicación](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="87531-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="87531-293">No</span><span class="sxs-lookup"><span data-stu-id="87531-293">No</span></span> |
| <span data-ttu-id="87531-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="87531-294">getDebugInfo</span></span> | <span data-ttu-id="87531-295">Especifica cuando los archivos de registro de hello Spark son copiado toohello utilizado por el clúster de HDInsight de almacenamiento de Azure (o) especificado por sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="87531-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="87531-296">Valores permitidos: Ninguno, Siempre o Error.</span><span class="sxs-lookup"><span data-stu-id="87531-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="87531-297">Valor predeterminado: Ninguno.</span><span class="sxs-lookup"><span data-stu-id="87531-297">Default value: None.</span></span> | <span data-ttu-id="87531-298">No</span><span class="sxs-lookup"><span data-stu-id="87531-298">No</span></span> |
| <span data-ttu-id="87531-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="87531-299">sparkJobLinkedService</span></span> | <span data-ttu-id="87531-300">Hola servicio vinculado de almacenamiento de Azure que contiene registros, las dependencias y archivo de trabajo de hello Spark.</span><span class="sxs-lookup"><span data-stu-id="87531-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="87531-301">Si no especifica un valor para esta propiedad, se usa almacenamiento de hello asociado con el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87531-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="87531-302">No</span><span class="sxs-lookup"><span data-stu-id="87531-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="87531-303">Estructura de carpetas</span><span class="sxs-lookup"><span data-stu-id="87531-303">Folder structure</span></span>
<span data-ttu-id="87531-304">Hola actividad Spark no es compatible con una secuencia de comandos en línea como Pig y realizar actividades de Hive.</span><span class="sxs-lookup"><span data-stu-id="87531-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="87531-305">Los trabajos de Spark también son más ampliable que los de Pig y Hive.</span><span class="sxs-lookup"><span data-stu-id="87531-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="87531-306">Para los trabajos de Spark, puede proporcionar varias dependencias, como paquetes (ubicados en java Hola CLASSPATH), python archivos jar (ubicados en hello PYTHONPATH) y cualquier otro archivo.</span><span class="sxs-lookup"><span data-stu-id="87531-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="87531-307">Crear Hola siguiendo la estructura de carpetas en Hola Hola servicio vinculado de HDInsight al que hace referencia el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="87531-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="87531-308">A continuación, cargue los archivos dependientes toohello adecuado subcarpetas en carpeta de raíz de hello representado por **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="87531-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="87531-309">Por ejemplo, cargar subcarpeta de python archivos toohello pyFiles y jar archivos toohello archivos JAR subcarpeta de la carpeta raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="87531-310">En tiempo de ejecución, el servicio de factoría de datos espera Hola siguiendo la estructura de carpetas en hello almacenamiento de blobs de Azure:</span><span class="sxs-lookup"><span data-stu-id="87531-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="87531-311">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="87531-311">Path</span></span> | <span data-ttu-id="87531-312">Descripción</span><span class="sxs-lookup"><span data-stu-id="87531-312">Description</span></span> | <span data-ttu-id="87531-313">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="87531-313">Required</span></span> | <span data-ttu-id="87531-314">Escriba</span><span class="sxs-lookup"><span data-stu-id="87531-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="87531-315">.</span><span class="sxs-lookup"><span data-stu-id="87531-315">.</span></span> | <span data-ttu-id="87531-316">ruta de acceso de Hello raíz del trabajo de Spark hello en el servicio vinculado de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="87531-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="87531-317">Sí</span><span class="sxs-lookup"><span data-stu-id="87531-317">Yes</span></span> | <span data-ttu-id="87531-318">Carpeta</span><span class="sxs-lookup"><span data-stu-id="87531-318">Folder</span></span> |
| <span data-ttu-id="87531-319">&lt;Definida por el usuario&gt;</span><span class="sxs-lookup"><span data-stu-id="87531-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="87531-320">ruta de acceso de Hola que señala toohello archivo de entrada de trabajo de Spark Hola</span><span class="sxs-lookup"><span data-stu-id="87531-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="87531-321">Sí</span><span class="sxs-lookup"><span data-stu-id="87531-321">Yes</span></span> | <span data-ttu-id="87531-322">Archivo</span><span class="sxs-lookup"><span data-stu-id="87531-322">File</span></span> |
| <span data-ttu-id="87531-323">./jars</span><span class="sxs-lookup"><span data-stu-id="87531-323">./jars</span></span> | <span data-ttu-id="87531-324">Todos los archivos en esta carpeta se cargan y se colocan en classpath de java de Hola de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="87531-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="87531-325">No</span><span class="sxs-lookup"><span data-stu-id="87531-325">No</span></span> | <span data-ttu-id="87531-326">Carpeta</span><span class="sxs-lookup"><span data-stu-id="87531-326">Folder</span></span> |
| <span data-ttu-id="87531-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="87531-327">./pyFiles</span></span> | <span data-ttu-id="87531-328">Todos los archivos en esta carpeta se cargan y se colocan en hello PYTHONPATH de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="87531-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="87531-329">No</span><span class="sxs-lookup"><span data-stu-id="87531-329">No</span></span> | <span data-ttu-id="87531-330">Carpeta</span><span class="sxs-lookup"><span data-stu-id="87531-330">Folder</span></span> |
| <span data-ttu-id="87531-331">./files</span><span class="sxs-lookup"><span data-stu-id="87531-331">./files</span></span> | <span data-ttu-id="87531-332">Todos los archivos de esta carpeta se cargan y se colocan en el directorio de trabajo del ejecutor.</span><span class="sxs-lookup"><span data-stu-id="87531-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="87531-333">No</span><span class="sxs-lookup"><span data-stu-id="87531-333">No</span></span> | <span data-ttu-id="87531-334">Carpeta</span><span class="sxs-lookup"><span data-stu-id="87531-334">Folder</span></span> |
| <span data-ttu-id="87531-335">./archives</span><span class="sxs-lookup"><span data-stu-id="87531-335">./archives</span></span> | <span data-ttu-id="87531-336">Todos los archivos de esta carpeta están sin comprimir.</span><span class="sxs-lookup"><span data-stu-id="87531-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="87531-337">No</span><span class="sxs-lookup"><span data-stu-id="87531-337">No</span></span> | <span data-ttu-id="87531-338">Carpeta</span><span class="sxs-lookup"><span data-stu-id="87531-338">Folder</span></span> |
| <span data-ttu-id="87531-339">./logs</span><span class="sxs-lookup"><span data-stu-id="87531-339">./logs</span></span> | <span data-ttu-id="87531-340">carpeta de Hola donde se almacenan los registros del clúster de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="87531-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="87531-341">No</span><span class="sxs-lookup"><span data-stu-id="87531-341">No</span></span> | <span data-ttu-id="87531-342">Carpeta</span><span class="sxs-lookup"><span data-stu-id="87531-342">Folder</span></span> |

<span data-ttu-id="87531-343">Este es un ejemplo de un almacenamiento que contiene dos archivos de trabajo de Spark en hello almacenamiento de blobs de Azure al que hace referencia Hola servicio vinculado de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="87531-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

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
