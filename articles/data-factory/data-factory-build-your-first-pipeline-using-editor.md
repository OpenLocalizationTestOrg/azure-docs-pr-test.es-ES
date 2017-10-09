---
title: "aaaBuild su primera factoría de datos (portal de Azure) | Documentos de Microsoft"
description: "En este tutorial, creará una canalización de factoría de datos de Azure de ejemplo mediante el Editor de generador de datos en hello portal de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="68bf7-103">Tutorial: Compilación de la primera instancia de Azure Data Factory con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="68bf7-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68bf7-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="68bf7-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="68bf7-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="68bf7-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="68bf7-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="68bf7-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="68bf7-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68bf7-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="68bf7-108">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="68bf7-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="68bf7-109">API DE REST</span><span class="sxs-lookup"><span data-stu-id="68bf7-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="68bf7-110">En este artículo, aprenderá cómo toouse [portal de Azure](https://portal.azure.com/) toocreate su primera factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="68bf7-111">tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="68bf7-112">canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="68bf7-113">Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce.</span><span class="sxs-lookup"><span data-stu-id="68bf7-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="68bf7-114">canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="68bf7-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="68bf7-115">canalización de datos de Hello en este tutorial transforma los datos de salida de tooproduce de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="68bf7-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="68bf7-116">Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="68bf7-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="68bf7-117">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="68bf7-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="68bf7-118">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="68bf7-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="68bf7-119">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="68bf7-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68bf7-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="68bf7-120">Prerequisites</span></span>
1. <span data-ttu-id="68bf7-121">Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="68bf7-122">En este artículo no proporciona una información general conceptual de hello servicio Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="68bf7-123">Se recomienda que pase por [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo para obtener una descripción detallada del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="68bf7-124">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="68bf7-124">Create data factory</span></span>
<span data-ttu-id="68bf7-125">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="68bf7-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="68bf7-126">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="68bf7-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="68bf7-127">Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de salida de tooproduct de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="68bf7-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="68bf7-128">Puede empezar con la creación de factoría de datos de hello en este paso.</span><span class="sxs-lookup"><span data-stu-id="68bf7-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="68bf7-129">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68bf7-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68bf7-130">Haga clic en **NEW** en el menú de la izquierda hello, haga clic en **datos + análisis**y haga clic en **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Hoja Creación](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="68bf7-132">Hola **factoría de datos** hoja, escriba **GetStartedDF** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="68bf7-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Hoja Nueva Factoría de datos](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="68bf7-134">nombre de Hola Hola Azure factoría de datos debe ser **único global**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="68bf7-135">Si recibe el error hello: **nombre de generador de datos "GetStartedDF" no está disponible**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="68bf7-136">Cambie el nombre Hola Hola factoría de datos (por ejemplo, yournameGetStartedDF) e intente crear de nuevo.</span><span class="sxs-lookup"><span data-stu-id="68bf7-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="68bf7-137">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="68bf7-138">nombre de Hola Hola factoría de datos se puede registrar como un **DNS** asigne un nombre en el futuro de hello y, por tanto, se convierten en visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="68bf7-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="68bf7-139">Seleccione hello **suscripción de Azure** donde desea Hola datos generador toobe creado.</span><span class="sxs-lookup"><span data-stu-id="68bf7-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="68bf7-140">Seleccione un **grupo de recursos** existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="68bf7-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="68bf7-141">Para ver tutorial Hola, cree un grupo de recursos denominado: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="68bf7-142">Seleccione hello **ubicación** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="68bf7-143">Solo las regiones compatibles con hello servicio factoría de datos se muestran en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="68bf7-144">Seleccione **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="68bf7-145">Haga clic en **crear** en hello **factoría de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="68bf7-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="68bf7-146">instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="68bf7-147">En el panel de hello, ve Hola siguiente icono con el estado: implementación factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Creación de estado de la factoría de datos](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="68bf7-149">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="68bf7-149">Congratulations!</span></span> <span data-ttu-id="68bf7-150">Ya creó correctamente su primera factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="68bf7-151">Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Hoja de la Factoría de datos](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="68bf7-153">Antes de crear una canalización de factoría de datos de hello, necesita toocreate algunas entidades de la factoría de datos en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="68bf7-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="68bf7-154">En primer lugar crear servicios vinculados toolink datos almacenes/calcula tooyour almacenarán, definen la entrada y salida de datos de entrada/salida de toorepresent de conjuntos de datos en almacenes de datos vinculado como los datos, a continuación, crear canalización Hola con una actividad que usa estos conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="68bf7-155">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="68bf7-155">Create linked services</span></span>
<span data-ttu-id="68bf7-156">En este paso, vincular su cuenta de almacenamiento de Azure y un generador de datos a petición tooyour de clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="68bf7-157">Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="68bf7-158">Hola servicio vinculado de HDInsight es toorun usa un script de Hive especificado en la actividad de hello de canalización de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="68bf7-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="68bf7-159">Identificar las actividades que [almacén de datos](data-factory-data-movement-activities.md)/[servicios de proceso](data-factory-compute-linked-services.md) se usan en el escenario y vincular esos factoría de datos de servicios toohello mediante la creación de servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="68bf7-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="68bf7-160">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="68bf7-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="68bf7-161">En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="68bf7-162">En este tutorial, utilice Hola misma cuenta de almacenamiento de Azure hello HQL y datos de entrada/salida de toostore los archivos de scripts.</span><span class="sxs-lookup"><span data-stu-id="68bf7-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="68bf7-163">Haga clic en **autor e implementar** en hello **factoría de datos** hoja para **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="68bf7-164">Debería ver Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-164">You should see hello Data Factory Editor.</span></span>

   ![Icono Crear e implementar](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="68bf7-166">Haga clic en **Nuevo almacén de datos** y elija **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nuevo almacén de datos - Azure Storage - menú](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="68bf7-168">Debería ver Hola script JSON para crear un almacenamiento de Azure vinculada servicio en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Servicio vinculado de Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="68bf7-170">Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de almacenamiento de Azure y **clave de cuenta** por clave de acceso de Hola de hello cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="68bf7-171">toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="68bf7-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="68bf7-172">Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Botón Implementar](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="68bf7-174">Después de hello servicio vinculado se ha implementado correctamente, Hola **Draft-1** ventana debería desaparecer y verá **AzureStorageLinkedService** en vista de árbol de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="68bf7-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Servicio vinculado de Almacenamiento en el menú](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="68bf7-176">Creación de un servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="68bf7-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="68bf7-177">En este paso, vincular un generador de datos a petición tooyour de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68bf7-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="68bf7-178">clúster de HDInsight de Hello automáticamente está creado en tiempo de ejecución y eliminar después de hacerlo inactivos y procesamiento para el período de tiempo especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="68bf7-179">Hola **Editor de generador de datos**, haga clic en **... Más** y en **Nuevo proceso**; después, seleccione **On-demand HDInsight cluster** (Clúster de HDInsight a petición).</span><span class="sxs-lookup"><span data-stu-id="68bf7-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nuevo proceso](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="68bf7-181">Copie y pegue Hola siguiente fragmento de código toohello **Draft-1** ventana.</span><span class="sxs-lookup"><span data-stu-id="68bf7-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="68bf7-182">fragmento JSON de Hello describe propiedades Hola Hola toocreate usado clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="68bf7-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="68bf7-183">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="68bf7-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="68bf7-184">Propiedad</span><span class="sxs-lookup"><span data-stu-id="68bf7-184">Property</span></span> | <span data-ttu-id="68bf7-185">Descripción</span><span class="sxs-lookup"><span data-stu-id="68bf7-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="68bf7-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="68bf7-186">ClusterSize</span></span> |<span data-ttu-id="68bf7-187">Especifica el tamaño de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68bf7-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="68bf7-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="68bf7-188">TimeToLive</span></span> | <span data-ttu-id="68bf7-189">Especifica ese tiempo de inactividad de hello para el clúster de HDInsight de hello, antes de eliminarla.</span><span class="sxs-lookup"><span data-stu-id="68bf7-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="68bf7-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="68bf7-190">linkedServiceName</span></span> | <span data-ttu-id="68bf7-191">Especifica la cuenta de almacenamiento de Hola que es toostore usado Hola registros generados por HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68bf7-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="68bf7-192">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="68bf7-192">Note hello following points:</span></span>

   * <span data-ttu-id="68bf7-193">Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello JSON.</span><span class="sxs-lookup"><span data-stu-id="68bf7-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="68bf7-194">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="68bf7-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="68bf7-195">Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="68bf7-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="68bf7-196">Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="68bf7-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="68bf7-197">clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="68bf7-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="68bf7-198">HDInsight no elimine este contenedor cuando se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="68bf7-199">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="68bf7-199">This behavior is by design.</span></span> <span data-ttu-id="68bf7-200">Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez se procesa un segmento, a menos que haya un clúster existente activo (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="68bf7-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="68bf7-201">clúster de Hola se elimina automáticamente cuando se realiza un procesamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="68bf7-202">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="68bf7-203">Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="68bf7-204">nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="68bf7-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="68bf7-205">Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="68bf7-206">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="68bf7-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="68bf7-207">Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Implementación de servicio vinculado de HDInsight a petición](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="68bf7-209">Confirme que ve ambos **AzureStorageLinkedService** y **HDInsightOnDemandLinkedService** en vista de árbol de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="68bf7-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Vista de árbol con servicios vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="68bf7-211">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="68bf7-211">Create datasets</span></span>
<span data-ttu-id="68bf7-212">En este paso, creación de conjuntos de datos toorepresent Hola entrada y salida de datos para el procesamiento de Hive.</span><span class="sxs-lookup"><span data-stu-id="68bf7-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="68bf7-213">Estos conjuntos de datos, consulte toohello **AzureStorageLinkedService** ha creado anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="68bf7-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="68bf7-214">Hola tooan de puntos de servicio vinculado cuenta de almacenamiento de Azure y los conjuntos de datos especifiquen contenedor, carpeta, nombre de archivo en el almacenamiento de Hola que contiene la entrada y salida de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="68bf7-215">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="68bf7-215">Create input dataset</span></span>
1. <span data-ttu-id="68bf7-216">Hola **Editor de generador de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y seleccione **almacenamiento de blobs de Azure**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nuevo conjunto de datos](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="68bf7-218">Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="68bf7-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="68bf7-219">En el fragmento JSON de hello, desea crear un conjunto de datos denominado **AzureBlobInput** que representa los datos de entrada para una actividad de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="68bf7-220">Además, especifica que los datos de entrada de Hola se encuentran en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="68bf7-221">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="68bf7-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="68bf7-222">Propiedad</span><span class="sxs-lookup"><span data-stu-id="68bf7-222">Property</span></span> | <span data-ttu-id="68bf7-223">Descripción</span><span class="sxs-lookup"><span data-stu-id="68bf7-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="68bf7-224">type</span><span class="sxs-lookup"><span data-stu-id="68bf7-224">type</span></span> |<span data-ttu-id="68bf7-225">propiedad de tipo Hello se establece demasiado**AzureBlob** porque los datos residen en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="68bf7-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="68bf7-226">linkedServiceName</span></span> |<span data-ttu-id="68bf7-227">Hace referencia a toohello **AzureStorageLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="68bf7-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="68bf7-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="68bf7-228">folderPath</span></span> | <span data-ttu-id="68bf7-229">Especifica el blob de hello **contenedor** hello y **carpeta** que contiene la entrada de blobs.</span><span class="sxs-lookup"><span data-stu-id="68bf7-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="68bf7-230">fileName</span><span class="sxs-lookup"><span data-stu-id="68bf7-230">fileName</span></span> |<span data-ttu-id="68bf7-231">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="68bf7-231">This property is optional.</span></span> <span data-ttu-id="68bf7-232">Si se omite esta propiedad, se seleccionan todos los archivos de Hola de hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="68bf7-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="68bf7-233">En este tutorial, solo Hola **input.log** se procesa.</span><span class="sxs-lookup"><span data-stu-id="68bf7-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="68bf7-234">type</span><span class="sxs-lookup"><span data-stu-id="68bf7-234">type</span></span> |<span data-ttu-id="68bf7-235">archivos de registro de Hello están en formato de texto, por lo que usamos **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="68bf7-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="68bf7-236">columnDelimiter</span></span> |<span data-ttu-id="68bf7-237">columnas en los archivos de registro de hello se delimitan mediante **carácter de coma (`,`)**</span><span class="sxs-lookup"><span data-stu-id="68bf7-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="68bf7-238">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="68bf7-238">frequency/interval</span></span> |<span data-ttu-id="68bf7-239">la frecuencia debe establecer demasiado**mes** y el intervalo es **1**, lo que significa que Hola entrada sectores están disponibles cada mes.</span><span class="sxs-lookup"><span data-stu-id="68bf7-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="68bf7-240">external</span><span class="sxs-lookup"><span data-stu-id="68bf7-240">external</span></span> | <span data-ttu-id="68bf7-241">Esta propiedad se establece demasiado**true** si no se generan datos de entrada de hello esta canalización.</span><span class="sxs-lookup"><span data-stu-id="68bf7-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="68bf7-242">En este tutorial, hello input.log no genera archivo esta canalización, por lo que establecemos Hola propiedad tootrue.</span><span class="sxs-lookup"><span data-stu-id="68bf7-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="68bf7-243">Para más información acerca de estas propiedades JSON, consulte el [artículo sobre el conector de blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="68bf7-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="68bf7-244">Haga clic en **implementar** en el conjunto de datos de toodeploy Hola que acaba de crear la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="68bf7-245">Debería ver el conjunto de datos de hello en vista de árbol de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="68bf7-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="68bf7-246">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="68bf7-246">Create output dataset</span></span>
<span data-ttu-id="68bf7-247">Ahora, cree Hola salida dataset toorepresent Hola salida datos almacenados en hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="68bf7-248">Hola **Editor de generador de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y seleccione **almacenamiento de blobs de Azure**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="68bf7-249">Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="68bf7-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="68bf7-250">En el fragmento JSON de hello, desea crear un conjunto de datos denominado **AzureBlobOutput**y especificar la estructura de Hola de datos de hello generada por script de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="68bf7-251">Además, se especifica que los resultados de Hola se almacenen en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="68bf7-252">Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se genera mensualmente.</span><span class="sxs-lookup"><span data-stu-id="68bf7-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    <span data-ttu-id="68bf7-253">Vea **crear conjunto de datos de entrada de hello** sección para obtener una descripción de estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="68bf7-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="68bf7-254">No establezca propiedad externa hello en un conjunto de datos de salida como conjunto de datos de hello es generado por el servicio de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="68bf7-255">Haga clic en **implementar** en el conjunto de datos de toodeploy Hola que acaba de crear la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="68bf7-256">Compruebe que ese conjunto de datos de Hola se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="68bf7-256">Verify that hello dataset is created successfully.</span></span>

    ![Vista de árbol con servicios vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="68bf7-258">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="68bf7-258">Create pipeline</span></span>
<span data-ttu-id="68bf7-259">En este paso, creará la primera canalización con una actividad **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="68bf7-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="68bf7-260">Segmento de entrada está disponible mensual (frecuencia: mes, intervalo: 1), segmento de salida se genera mensualmente y Hola programador propiedad actividad hello también está configurada toomonthly.</span><span class="sxs-lookup"><span data-stu-id="68bf7-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="68bf7-261">debe coincidir con la configuración de Hello para el conjunto de datos de salida de Hola y el programador de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="68bf7-262">Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="68bf7-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="68bf7-263">Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada.</span><span class="sxs-lookup"><span data-stu-id="68bf7-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="68bf7-264">propiedades de Hello utilizadas en hello después de JSON se explican al final de Hola de esta sección.</span><span class="sxs-lookup"><span data-stu-id="68bf7-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="68bf7-265">Hola **Editor de generador de datos**, haga clic en **puntos suspensivos (...) Más comandos** y, a continuación, haga clic en **nueva canalización**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![Botón Nueva canalización](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="68bf7-267">Copie y pegue Hola después de la ventana de toohello Draft-1 de fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="68bf7-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="68bf7-268">Reemplace **storageaccountname** con el nombre de Hola de su cuenta de almacenamiento en hello JSON.</span><span class="sxs-lookup"><span data-stu-id="68bf7-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="68bf7-269">En el fragmento JSON de hello, desea crear una canalización que consta de una actividad única que usa Hive tooprocess datos en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68bf7-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="68bf7-270">archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **AzureStorageLinkedService**) y en  **secuencia de comandos** carpeta en el contenedor de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="68bf7-271">Hola **define** sección es la configuración de en tiempo de ejecución de hello toospecify utilizado que se pasa el script de hive toohello como valores de configuración de Hive (por ejemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="68bf7-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="68bf7-272">Hola **iniciar** y **final** propiedades de canalización de hello especifica el periodo activo de Hola de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="68bf7-273">En JSON de la actividad de hello, especifique ese script de Hive Hola se ejecuta en proceso Hola especificado por hello **linkedServiceName** : **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="68bf7-274">Consulte la sección "JSON de canalización" en [canalizaciones y actividades de Data Factory de Azure](data-factory-create-pipelines.md) para obtener más información sobre propiedades JSON que se usan en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="68bf7-275">Confirmar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="68bf7-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="68bf7-276">**Input.log** archivo existe en hello **inputdata** carpeta de hello **adfgetstarted** contenedor Hola almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="68bf7-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="68bf7-277">**partitionweblogs.hql** archivo existe en hello **script** carpeta de hello **adfgetstarted** contenedor Hola almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="68bf7-278">Requisito previo de hello completa los pasos de hello [Tutorial Introducción](data-factory-build-your-first-pipeline.md) si no ve estos archivos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="68bf7-279">Confirme que ha reemplazado **storageaccountname** con el nombre de Hola de su cuenta de almacenamiento en Hola de canalización JSON.</span><span class="sxs-lookup"><span data-stu-id="68bf7-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="68bf7-280">Haga clic en **implementar** en la canalización de hello toodeploy la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="68bf7-281">Desde hello **iniciar** y **final** veces se establecen en los último hello y **isPaused** es toofalse de conjunto, canalización Hola ejecuciones (actividad de canalización de hello) inmediatamente después de implementar.</span><span class="sxs-lookup"><span data-stu-id="68bf7-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="68bf7-282">Confirme que ve canalización hello en la vista de árbol de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Vista de árbol con canalización](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="68bf7-284">Enhorabuena, ya creó correctamente su primera canalización.</span><span class="sxs-lookup"><span data-stu-id="68bf7-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="68bf7-285">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="68bf7-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="68bf7-286">Supervisión de una canalización desde la vista de diagrama</span><span class="sxs-lookup"><span data-stu-id="68bf7-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="68bf7-287">Haga clic en **X** tooclose Editor de generador de datos hojas toonavigate hacer copia de hoja de la factoría de datos de toohello y haga clic en **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Icono Diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="68bf7-289">En la vista de diagrama de hello, verá información general de las canalizaciones de Hola y conjuntos de datos usados en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="68bf7-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Vista de diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="68bf7-291">tooview todas las actividades de canalización de hello, menú contextual "canalización" Hola, diagrama y haga clic en abrir canalización.</span><span class="sxs-lookup"><span data-stu-id="68bf7-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menú Abrir canalización](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="68bf7-293">Confirme que ve actividad HDInsightHive de hello en canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Vista Abrir canalización](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="68bf7-295">toonavigate realizar copias toohello vista anterior, haga clic en **factoría de datos** en el menú de la ruta de navegación de hello en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="68bf7-296">Hola **vista de diagrama**, haga doble clic en el conjunto de datos de hello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="68bf7-297">Confirme que dicho sector Hola está en **listo** estado.</span><span class="sxs-lookup"><span data-stu-id="68bf7-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="68bf7-298">Pueden tardar unos minutos para tooshow de segmento de hello en estado listo.</span><span class="sxs-lookup"><span data-stu-id="68bf7-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="68bf7-299">Si no se realiza después de que espere unos instantes, ver si el archivo de entrada de hello (input.log) colocado en el contenedor de derecho de hello (adfgetstarted) y la carpeta (inputdata).</span><span class="sxs-lookup"><span data-stu-id="68bf7-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Segmento de entrada con estado Listo](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="68bf7-301">Haga clic en **X** tooclose **AzureBlobInput** hoja.</span><span class="sxs-lookup"><span data-stu-id="68bf7-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="68bf7-302">Hola **vista de diagrama**, haga doble clic en el conjunto de datos de hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="68bf7-303">Vea dicho sector Hola que se está procesando actualmente.</span><span class="sxs-lookup"><span data-stu-id="68bf7-303">You see that hello slice that is currently being processed.</span></span>

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="68bf7-305">Cuando se realiza el procesamiento, verá que el segmento de hello en **listo** estado.</span><span class="sxs-lookup"><span data-stu-id="68bf7-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Dataset](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="68bf7-307">La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="68bf7-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="68bf7-308">Por consiguiente, esperan canalización Hola tardar demasiado **aproximadamente 30 minutos** tooprocess Hola segmento.</span><span class="sxs-lookup"><span data-stu-id="68bf7-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="68bf7-309">Cuando se encuentra el segmento de hello en **listo** de estado, compruebe hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="68bf7-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![datos de salida](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="68bf7-311">Haga clic en hello segmento toosee detalles sobre él en un **el segmento de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="68bf7-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Detalles de segmento de datos](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="68bf7-313">Haga clic en una actividad que se ejecutan en hello **lista ejecuta la actividad** toosee detalles sobre la actividad de ejecución (actividad de Hive en nuestro escenario) un **detalles de ejecución de la actividad** ventana.</span><span class="sxs-lookup"><span data-stu-id="68bf7-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Detalles de ejecución de actividad](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="68bf7-315">Desde archivos de registro de hello, puede ver información de estado y de consulta de Hive de Hola que se ejecutó.</span><span class="sxs-lookup"><span data-stu-id="68bf7-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="68bf7-316">Estos registros son útiles para solucionar cualquier problema.</span><span class="sxs-lookup"><span data-stu-id="68bf7-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="68bf7-317">Para más información, consulte el artículo [Supervisión y administración de canalizaciones mediante las hojas del Portal de Azure](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="68bf7-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68bf7-318">archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente.</span><span class="sxs-lookup"><span data-stu-id="68bf7-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="68bf7-319">Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="68bf7-320">Supervisión de una canalización con la Aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="68bf7-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="68bf7-321">También puede utilizar el Monitor de & Administrar aplicación toomonitor sus canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="68bf7-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="68bf7-322">Para más información acerca del uso de esta aplicación, consulte [Supervisión y administración de canalizaciones de Azure Data Factory mediante la nueva Aplicación de supervisión y administración](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="68bf7-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="68bf7-323">Haga clic en **Monitor & administrar** de mosaico en la página principal de saludo de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="68bf7-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![Icono Supervisión y administración](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="68bf7-325">Debería ver la **aplicación de supervisión y administración**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="68bf7-326">Hola de cambio **hora de inicio** y **hora de finalización** toomatch inicio y finalización de la canalización y haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![Aplicación de supervisión y administración](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="68bf7-328">Seleccione una ventana actividad Hola **Windows actividad** lista toosee detalles sobre él.</span><span class="sxs-lookup"><span data-stu-id="68bf7-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Detalles de ventana de actividad](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="68bf7-330">Resumen</span><span class="sxs-lookup"><span data-stu-id="68bf7-330">Summary</span></span>
<span data-ttu-id="68bf7-331">En este tutorial, ha creado un datos tooprocess de factoría de datos de Azure mediante la ejecución de script de Hive en un clúster de hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68bf7-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="68bf7-332">Utiliza el Editor de generador de datos de Hola Hola toodo portal Azure Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="68bf7-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="68bf7-333">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="68bf7-334">Ha creado dos **servicios vinculados**:</span><span class="sxs-lookup"><span data-stu-id="68bf7-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="68bf7-335">**Almacenamiento de Azure** vinculado servicio toolink el almacenamiento de blobs de Azure que contiene la factoría de datos de archivos de entrada/salida toohello.</span><span class="sxs-lookup"><span data-stu-id="68bf7-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="68bf7-336">**HDInsight de Azure** toolink de servicio vinculado a petición una factoría de datos a petición toohello de clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="68bf7-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="68bf7-337">Factoría de datos de Azure crea un Hadoop de HDInsight los datos de entrada de tooprocess just-in-time de clúster y generan datos de salida.</span><span class="sxs-lookup"><span data-stu-id="68bf7-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="68bf7-338">Crea dos **conjuntos de datos**, que describen los datos de entrada y salidos de actividad de Hive de HDInsight en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="68bf7-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="68bf7-339">Ha creado una **canalización** con una actividad de **Hive de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="68bf7-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68bf7-340">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68bf7-340">Next Steps</span></span>
<span data-ttu-id="68bf7-341">En este artículo, creó una canalización con una actividad de transformación (actividad de HDInsight) que ejecuta un script de Hive en un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="68bf7-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="68bf7-342">toosee toouse una toocopy de datos de actividad de copia de un tooAzure de Blob de Azure SQL, vea [Tutorial: copiar los datos de un tooAzure de blobs de Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="68bf7-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="68bf7-343">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="68bf7-343">See Also</span></span>
| <span data-ttu-id="68bf7-344">Tema.</span><span class="sxs-lookup"><span data-stu-id="68bf7-344">Topic</span></span> | <span data-ttu-id="68bf7-345">Descripción</span><span class="sxs-lookup"><span data-stu-id="68bf7-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="68bf7-346">Procesos</span><span class="sxs-lookup"><span data-stu-id="68bf7-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="68bf7-347">En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa.</span><span class="sxs-lookup"><span data-stu-id="68bf7-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="68bf7-348">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="68bf7-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="68bf7-349">Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bf7-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="68bf7-350">Programación y ejecución con Data Factory</span><span class="sxs-lookup"><span data-stu-id="68bf7-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="68bf7-351">En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="68bf7-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="68bf7-352">Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="68bf7-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="68bf7-353">Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="68bf7-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
