---
title: "Tutorial: Crear una canalización con la actividad de copia mediante Visual Studio | Microsoft Docs"
description: "En este tutorial, creará una canalización de Data Factory de Azure con una actividad de copia mediante Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="c6b00-103">Tutorial: Crear una canalización con la actividad de copia mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6b00-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6b00-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6b00-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="c6b00-105">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="c6b00-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="c6b00-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c6b00-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="c6b00-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6b00-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="c6b00-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6b00-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="c6b00-109">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6b00-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="c6b00-110">API DE REST</span><span class="sxs-lookup"><span data-stu-id="c6b00-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="c6b00-111">API de .NET</span><span class="sxs-lookup"><span data-stu-id="c6b00-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="c6b00-112">En este artículo, aprenderá cómo toouse Hola toocreate de Microsoft Visual Studio una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="c6b00-113">Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c6b00-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="c6b00-114">En este tutorial, creará una canalización con una actividad en ella: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="c6b00-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="c6b00-115">actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="c6b00-116">Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c6b00-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c6b00-117">actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="c6b00-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="c6b00-118">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="c6b00-119">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="c6b00-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c6b00-120">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="c6b00-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c6b00-121">Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c6b00-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="c6b00-122">canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="c6b00-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="c6b00-123">Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6b00-124">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6b00-124">Prerequisites</span></span>
1. <span data-ttu-id="c6b00-125">Lea [Tutorial de introducción](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hello completa y artículo **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="c6b00-126">instancias de la factoría de datos de toocreate, debe ser miembro del programa Hola a [colaborador de la factoría de datos](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol en el nivel de grupo de recursos/suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="c6b00-127">Debe tener instalado en el equipo siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="c6b00-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="c6b00-128">Visual Studio 2013 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c6b00-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="c6b00-129">Descargue el SDK de Azure para Visual Studio 2013 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c6b00-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="c6b00-130">Navegue demasiado[página de descargas de Azure](https://azure.microsoft.com/downloads/) y haga clic en **VS 2013** o **VS 2015** en hello **.NET** sección.</span><span class="sxs-lookup"><span data-stu-id="c6b00-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="c6b00-131">Descargue el complemento de Data Factory de Azure más reciente de Hola para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="c6b00-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="c6b00-132">También puede actualizar Hola complemento mediante Hola pasos: en el menú de hello, haga clic en **herramientas** -> **extensiones y actualizaciones** -> **en línea**  ->  **Galería de visual Studio** -> **herramientas de generador de datos de Microsoft Azure para Visual Studio** -> **actualización**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="c6b00-133">Pasos</span><span class="sxs-lookup"><span data-stu-id="c6b00-133">Steps</span></span>
<span data-ttu-id="c6b00-134">Estos son los pasos de hello que realizar como parte de este tutorial:</span><span class="sxs-lookup"><span data-stu-id="c6b00-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="c6b00-135">Crear **servicios vinculados** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="c6b00-136">En este paso, se crean dos servicios vinculados del tipo Azure Storage y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c6b00-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="c6b00-137">Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c6b00-138">Crea un contenedor y cargar la cuenta de almacenamiento de datos toothis como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="c6b00-139">AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c6b00-140">datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c6b00-141">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó una tabla SQL en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="c6b00-142">Crear la entrada y salida **conjuntos de datos** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="c6b00-143">servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c6b00-144">Y el conjunto de datos de hello blob de entrada especifica el contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="c6b00-145">De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c6b00-146">Y conjunto de datos de tabla SQL de Hola salida especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c6b00-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="c6b00-147">Crear un **canalización** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="c6b00-148">En este paso, se crea una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="c6b00-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="c6b00-149">actividad de copia de Hello copia datos de un blob en la tabla de tooa de almacenamiento de blobs de Azure de hello en la base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="c6b00-150">Puede usar una actividad de copia en datos toocopy canalización desde cualquier origen compatibles tooany admitida el destino.</span><span class="sxs-lookup"><span data-stu-id="c6b00-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="c6b00-151">Para ver una lista de los almacenes de datos admitidos, consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c6b00-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="c6b00-152">Cree una **factoría de datos** de Azure al implementar entidades de Data Factory (servicios vinculados, conjuntos de datos o tablas y canalizaciones).</span><span class="sxs-lookup"><span data-stu-id="c6b00-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="c6b00-153">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6b00-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="c6b00-154">Inicie **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="c6b00-155">Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="c6b00-156">Debería ver Hola **nuevo proyecto** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="c6b00-157">Hola **nuevo proyecto** cuadro de diálogo, seleccione hello **DataFactory** plantilla y haga clic en **proyecto vacío de la factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Cuadro de diálogo Nuevo proyecto](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="c6b00-159">Especifique nombre Hola de proyecto de hello, la ubicación para la solución de Hola y el nombre de solución de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Explorador de soluciones](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="c6b00-161">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="c6b00-161">Create linked services</span></span>
<span data-ttu-id="c6b00-162">Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="c6b00-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="c6b00-163">En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6b00-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="c6b00-164">Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino).</span><span class="sxs-lookup"><span data-stu-id="c6b00-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="c6b00-165">Por lo tanto, se crean dos servicios vinculados del tipo AzureStorage y AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="c6b00-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="c6b00-166">Hola almacenamiento de Azure vinculados a los vínculos de servicio su factoría de datos de almacenamiento de Azure cuenta toohello.</span><span class="sxs-lookup"><span data-stu-id="c6b00-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c6b00-167">Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="c6b00-168">SQL Azure había vinculado a los vínculos de servicio su factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c6b00-169">datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c6b00-170">Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="c6b00-171">Servicios vinculados vinculan almacenes de datos o generador de datos de Azure de tooan de servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="c6b00-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="c6b00-172">Vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) de Hola a todos los orígenes y receptores admitidos por hello actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="c6b00-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="c6b00-173">Vea [servicios vinculados de proceso](data-factory-compute-linked-services.md) para lista de hello de servicios de proceso admitidos factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="c6b00-174">En este tutorial no se usan servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="c6b00-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="c6b00-175">Crear servicio vinculado de almacenamiento de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="c6b00-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="c6b00-176">En **el Explorador de soluciones**, haga clic en **servicios vinculados**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="c6b00-177">Hola **Agregar nuevo elemento** cuadro de diálogo, seleccione **servicio vinculado de almacenamiento de Azure** en lista de Hola y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Nuevo servicio vinculado](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="c6b00-179">Reemplace `<accountname>` y `<accountkey>`* con nombre Hola de su cuenta de almacenamiento de Azure y su clave.</span><span class="sxs-lookup"><span data-stu-id="c6b00-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Servicio vinculado de Almacenamiento de Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="c6b00-181">Guardar hello **AzureStorageLinkedService1.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="c6b00-182">Para obtener más información acerca de las propiedades JSON en definición de servicio vinculado de hello, consulte [conector del almacenamiento de blobs de Azure](data-factory-azure-blob-connector.md#linked-service-properties) artículo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="c6b00-183">Crear servicio de SQL Azure vinculado Hola</span><span class="sxs-lookup"><span data-stu-id="c6b00-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="c6b00-184">Haga doble clic en **servicios vinculados** nodo Hola **el Explorador de soluciones** nuevo, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="c6b00-185">Esta vez, seleccione **Servicios vinculados de SQL Azure** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="c6b00-186">Hola **AzureSqlLinkedService1.json archivo**, reemplace `<servername>`, `<databasename>`, `<username@servername>`, y `<password>` con nombres de su servidor SQL Azure, la base de datos, la cuenta de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c6b00-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="c6b00-187">Guardar hello **AzureSqlLinkedService1.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="c6b00-188">Para más información acerca de estas propiedades JSON, consulte [Conector de Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c6b00-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="c6b00-189">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="c6b00-189">Create datasets</span></span>
<span data-ttu-id="c6b00-190">En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="c6b00-191">En este paso, definirá dos conjuntos de datos con el nombre InputDataset y OutputDataset que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService1 y AzureSqlLinkedService1 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="c6b00-192">servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c6b00-193">Y conjunto de datos de blob de entrada de hello (InputDataset) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="c6b00-194">De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c6b00-195">Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c6b00-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="c6b00-196">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="c6b00-196">Create input dataset</span></span>
<span data-ttu-id="c6b00-197">En este paso, creará un conjunto de datos denominado InputDataset que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService1 vinculado servicio de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="c6b00-198">Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="c6b00-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="c6b00-199">En este tutorial, especifique un valor para el nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="c6b00-200">A continuación, use el término de Hola "tablas" en lugar de "conjuntos de datos".</span><span class="sxs-lookup"><span data-stu-id="c6b00-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="c6b00-201">Una tabla es un conjunto de datos rectangular y es Hola único tipo de conjunto de datos admitido ahora mismo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="c6b00-202">Haga clic en **tablas** en hello **el Explorador de soluciones**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="c6b00-203">Hola **Agregar nuevo elemento** cuadro de diálogo, seleccione **Azure Blob**y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="c6b00-204">Reemplazar texto JSON de hello con hello después de texto y guarde hello **AzureBlobLocation1.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
      "structure": [
        {
          "name": "FirstName",
          "type": "String"
        },
        {
          "name": "LastName",
          "type": "String"
        }
      ],
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    <span data-ttu-id="c6b00-205">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="c6b00-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c6b00-206">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c6b00-206">Property</span></span> | <span data-ttu-id="c6b00-207">Descripción</span><span class="sxs-lookup"><span data-stu-id="c6b00-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c6b00-208">type</span><span class="sxs-lookup"><span data-stu-id="c6b00-208">type</span></span> | <span data-ttu-id="c6b00-209">propiedad de tipo Hello se establece demasiado**AzureBlob** porque los datos residen en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="c6b00-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c6b00-210">linkedServiceName</span></span> | <span data-ttu-id="c6b00-211">Hace referencia a toohello **AzureStorageLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c6b00-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="c6b00-212">folderPath</span></span> | <span data-ttu-id="c6b00-213">Especifica el blob de hello **contenedor** hello y **carpeta** que contiene la entrada de blobs.</span><span class="sxs-lookup"><span data-stu-id="c6b00-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="c6b00-214">En este tutorial, adftutorial es el contenedor de blob de Hola y carpeta es la carpeta raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="c6b00-215">fileName</span><span class="sxs-lookup"><span data-stu-id="c6b00-215">fileName</span></span> | <span data-ttu-id="c6b00-216">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="c6b00-216">This property is optional.</span></span> <span data-ttu-id="c6b00-217">Si se omite esta propiedad, se seleccionan todos los archivos de hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="c6b00-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="c6b00-218">En este tutorial, **emp.txt** se especificó para hello nombre de archivo, por lo que sólo ese archivo se recoge para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="c6b00-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="c6b00-219">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="c6b00-219">format -> type</span></span> |<span data-ttu-id="c6b00-220">archivo de entrada de Hello es hello en formato de texto, por lo que usamos **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="c6b00-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c6b00-221">columnDelimiter</span></span> | <span data-ttu-id="c6b00-222">columnas de Hello en el archivo de entrada de Hola se delimitan mediante **carácter de coma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="c6b00-223">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="c6b00-223">frequency/interval</span></span> | <span data-ttu-id="c6b00-224">frecuencia de Hola se establece demasiado**hora** e intervalo está establecido demasiado**1**, lo que significa que Hola entrada sectores están disponibles **cada hora**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="c6b00-225">En otras palabras, Hola servicio Data Factory busca datos de entrada cada hora en carpeta de raíz de hello del contenedor de blobs (**adftutorial**) que especificó.</span><span class="sxs-lookup"><span data-stu-id="c6b00-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="c6b00-226">Busca datos Hola Hola canalización inicio y finalización horas, no antes o después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="c6b00-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="c6b00-227">external</span><span class="sxs-lookup"><span data-stu-id="c6b00-227">external</span></span> | <span data-ttu-id="c6b00-228">Esta propiedad se establece demasiado**true** si no se generan datos de hello esta canalización.</span><span class="sxs-lookup"><span data-stu-id="c6b00-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="c6b00-229">datos de entrada de Hello en este tutorial están en el archivo emp.txt de hello, que no se genera esta canalización, por lo que se establece esta propiedad tootrue.</span><span class="sxs-lookup"><span data-stu-id="c6b00-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="c6b00-230">Para más información acerca de estas propiedades JSON, consulte el [artículo sobre el conector de blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c6b00-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="c6b00-231">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="c6b00-231">Create output dataset</span></span>
<span data-ttu-id="c6b00-232">En este paso se crea un conjunto de datos de salida denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="c6b00-233">Este conjunto de datos señala tooa table de SQL de base de datos de SQL Azure de hello representado por **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="c6b00-234">Haga clic en **tablas** en hello **el Explorador de soluciones** nuevo, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="c6b00-235">Hola **Agregar nuevo elemento** cuadro de diálogo, seleccione **SQL Azure**y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="c6b00-236">Reemplazar texto JSON de hello con hello después de JSON y guardar hello **AzureSqlTableLocation1.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

  ```json
    {
     "name": "OutputDataset",
     "properties": {
       "structure": [
         {
           "name": "FirstName",
           "type": "String"
         },
         {
           "name": "LastName",
           "type": "String"
         }
       ],
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    <span data-ttu-id="c6b00-237">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="c6b00-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c6b00-238">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c6b00-238">Property</span></span> | <span data-ttu-id="c6b00-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="c6b00-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c6b00-240">type</span><span class="sxs-lookup"><span data-stu-id="c6b00-240">type</span></span> | <span data-ttu-id="c6b00-241">propiedad de tipo Hello se establece demasiado**AzureSqlTable** porque datos están la tabla de tooa copiado en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="c6b00-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c6b00-242">linkedServiceName</span></span> | <span data-ttu-id="c6b00-243">Hace referencia a toohello **AzureSqlLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c6b00-244">tableName</span><span class="sxs-lookup"><span data-stu-id="c6b00-244">tableName</span></span> | <span data-ttu-id="c6b00-245">Hola especificado **tabla** toowhich Hola datos se copian.</span><span class="sxs-lookup"><span data-stu-id="c6b00-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="c6b00-246">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="c6b00-246">frequency/interval</span></span> | <span data-ttu-id="c6b00-247">Hello frecuencia se establece demasiado**hora** y el intervalo es **1**, lo que significa que se producen los sectores de salida de hello **cada hora** entre el inicio de la canalización de Hola y de finalización veces, no antes o Después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="c6b00-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="c6b00-248">Hay tres columnas: **identificador**, **FirstName**, y **LastName** : en la tabla emp de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="c6b00-249">Id. es una columna de identidad, por lo que necesita solo toospecify **FirstName** y **LastName** aquí.</span><span class="sxs-lookup"><span data-stu-id="c6b00-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="c6b00-250">Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c6b00-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="c6b00-251">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="c6b00-251">Create pipeline</span></span>
<span data-ttu-id="c6b00-252">En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="c6b00-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="c6b00-253">Actualmente, el conjunto de datos de salida es qué unidades Hola programación.</span><span class="sxs-lookup"><span data-stu-id="c6b00-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="c6b00-254">En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="c6b00-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="c6b00-255">canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="c6b00-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="c6b00-256">Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="c6b00-257">Haga clic en **canalizaciones** en hello **el Explorador de soluciones**, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="c6b00-258">Seleccione **canalización de datos de copia** en hello **Agregar nuevo elemento** cuadro de diálogo y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="c6b00-259">Reemplazar Hola JSON con hello después de JSON y guardar hello **CopyActivity1.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="c6b00-260">En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="c6b00-261">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c6b00-262">En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="c6b00-263">Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="c6b00-264">Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="c6b00-265">Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c6b00-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c6b00-266">toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="c6b00-267">Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="c6b00-268">Puede especificar sólo parte de fecha de Hola y omitir la parte de hora de Hola de hello fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="c6b00-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="c6b00-269">Por ejemplo, "2016-02-03", que es equivalente demasiado "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="c6b00-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="c6b00-270">Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c6b00-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c6b00-271">Por ejemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c6b00-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="c6b00-272">Hola **final** tiempo es opcional, pero se usa en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c6b00-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="c6b00-273">Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="c6b00-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="c6b00-274">canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.</span><span class="sxs-lookup"><span data-stu-id="c6b00-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="c6b00-275">En el anterior ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.</span><span class="sxs-lookup"><span data-stu-id="c6b00-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="c6b00-276">Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c6b00-277">Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c6b00-278">Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="c6b00-279">Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="c6b00-280">Publicación e implementación de las entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="c6b00-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="c6b00-281">En este paso, se publican las entidades de Data Factory (servicios vinculados, conjuntos de datos y canalización) que se crearon anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="c6b00-282">También especificar nombre de Hola de hello toobe de factoría de datos nuevo creado toohold estas entidades.</span><span class="sxs-lookup"><span data-stu-id="c6b00-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="c6b00-283">Haga clic en el proyecto en el Explorador de soluciones de Hola y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="c6b00-284">Si ve **iniciar sesión en la cuenta de Microsoft tooyour** cuadro de diálogo, escriba sus credenciales de cuenta de hello que tenga la suscripción de Azure y haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="c6b00-285">Debería ver Hola después el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="c6b00-285">You should see hello following dialog box:</span></span>
   
   ![Cuadro de diálogo Publicar](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="c6b00-287">En la página de generador de datos de configuración de hello, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6b00-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="c6b00-288">Seleccione la opción **Crear la nueva factoría de datos** .</span><span class="sxs-lookup"><span data-stu-id="c6b00-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="c6b00-289">Escriba **VSTutorialFactory** para **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="c6b00-290">nombre de Hola Hola Azure factoría de datos debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="c6b00-291">Si recibe un error indicando nombre Hola de factoría de datos al publicar, cambiar nombre de Hola de factoría de datos de hello (por ejemplo, yournameVSTutorialFactory) e intente publicar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="c6b00-292">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="c6b00-293">Seleccione la suscripción de Azure para hello **suscripción** campo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="c6b00-294">Si no ve ninguna suscripción, asegúrese de que inició sesión mediante una cuenta que sea un administrador o Coadministrador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="c6b00-295">Seleccione hello **grupo de recursos** para toobe de factoría de datos de hello creado.</span><span class="sxs-lookup"><span data-stu-id="c6b00-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="c6b00-296">Seleccione hello **región** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="c6b00-297">Solo las regiones compatibles con hello servicio factoría de datos se muestran en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="c6b00-298">Haga clic en **siguiente** tooswitch toohello **publicar elementos** página.</span><span class="sxs-lookup"><span data-stu-id="c6b00-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Configurar página de Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="c6b00-300">Hola **publicar elementos** página, asegúrese de que todas las factorías de datos de entidades están seleccionadas y haga clic en Hola **siguiente** tooswitch toohello **resumen** página.</span><span class="sxs-lookup"><span data-stu-id="c6b00-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Página Publicar elementos](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="c6b00-302">Revise el resumen de Hola y haga clic en **siguiente** Hola de proceso y la vista de la implementación del hello toostart **estado de implementación**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Página Publicar resumen](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="c6b00-304">Hola **estado de implementación** página, debería ver estado de Hola Hola del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="c6b00-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="c6b00-305">Después de que se realice la implementación de hello, haga clic en Finalizar.</span><span class="sxs-lookup"><span data-stu-id="c6b00-305">Click Finish after hello deployment is done.</span></span>
 
   ![Página Estado de la implementación](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="c6b00-307">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="c6b00-307">Note hello following points:</span></span> 

* <span data-ttu-id="c6b00-308">Si recibe el error hello: "esta suscripción no está registrado toouse de espacio de nombres Microsoft.DataFactory", siga uno de los procedimientos de Hola e intente publicar de nuevo:</span><span class="sxs-lookup"><span data-stu-id="c6b00-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="c6b00-309">En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="c6b00-310">Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado.</span><span class="sxs-lookup"><span data-stu-id="c6b00-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="c6b00-311">Inicio de sesión mediante Hola suscripción de Azure en hello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="c6b00-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="c6b00-312">Esta acción registra automáticamente proveedor Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="c6b00-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="c6b00-313">nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, se convierten en visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6b00-314">instancias de la factoría de datos de toocreate, deberá toobe un administrador o Coadministrador de hello suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="c6b00-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c6b00-315">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="c6b00-315">Monitor pipeline</span></span>
<span data-ttu-id="c6b00-316">Desplácese toohello página de inicio de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="c6b00-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="c6b00-317">Inicie sesión demasiado[portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6b00-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c6b00-318">Haga clic en **más servicios** en Hola menú izquierdo y haga clic en **factorías de datos**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Examinar factorías de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="c6b00-320">Comience a escribir el nombre de saludo de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-320">Start typing hello name of your data factory.</span></span>

    ![Nombre de la factoría de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="c6b00-322">Haga clic en la factoría de datos en la página Hola resultados lista toosee Hola principal de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Página principal de Factoría de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="c6b00-324">Siga las instrucciones de [supervisar conjuntos de datos y canalización](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor canalización de Hola y conjuntos de datos ha creado en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c6b00-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="c6b00-325">Actualmente, Visual Studio no permite supervisar canalizaciones de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6b00-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="c6b00-326">Resumen</span><span class="sxs-lookup"><span data-stu-id="c6b00-326">Summary</span></span>
<span data-ttu-id="c6b00-327">En este tutorial, ha creado un datos toocopy de factoría de datos de Azure desde una base de datos de SQL Azure de tooan de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="c6b00-328">Ha utilizado la factoría de datos de Visual Studio toocreate hello, servicios vinculados, conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="c6b00-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="c6b00-329">Estos son los pasos de alto nivel de hello realizadas en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="c6b00-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="c6b00-330">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c6b00-331">Ha creado **servicios vinculados**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="c6b00-332">Un **el almacenamiento de Azure** vinculado toolink de servicio de la cuenta de almacenamiento de Azure que contiene datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c6b00-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="c6b00-333">Un **SQL Azure** vinculado toolink de servicio en la base de datos de SQL Azure que contiene los datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c6b00-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="c6b00-334">Ha creado **conjuntos de datos**que describen los datos de entrada y salida para las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="c6b00-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="c6b00-335">Ha creado una **canalización** con una **actividad de copia** con un origen **BlobSource** y un receptor **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="c6b00-336">toosee toouse una actividad de Hive de HDInsight tootransform de datos mediante el clúster de HDInsight de Azure, vea [ Tutorial: generar los datos primera canalización tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="c6b00-337">Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="c6b00-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c6b00-338">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="c6b00-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="c6b00-339">Presentación de todas las factorías de datos en el explorador de servidores</span><span class="sxs-lookup"><span data-stu-id="c6b00-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="c6b00-340">Esta sección describe cómo toouse Hola Explorador de servidores en Visual Studio tooview todos los generadores de datos de hello en su suscripción de Azure y crear un proyecto de Visual Studio basado en un generador de datos existente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="c6b00-341">En **Visual Studio**, haga clic en **vista** en Hola menú y haga clic en **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="c6b00-342">En la ventana del explorador de servidores de hello, expanda **Azure** y expanda **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="c6b00-343">Si ve **iniciar sesión en tooVisual Studio**, escriba Hola **cuenta** asociada a su suscripción de Azure y haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="c6b00-344">Escriba la **contraseña** y haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="c6b00-345">Visual Studio intenta tooget información acerca de todos los generadores de datos de Azure en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="c6b00-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="c6b00-346">Vea Estado Hola de esta operación en hello **lista de tareas del generador de datos** ventana.</span><span class="sxs-lookup"><span data-stu-id="c6b00-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Explorador de servidores](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="c6b00-348">Creación de un proyecto de Visual Studio para una factoría de datos existente</span><span class="sxs-lookup"><span data-stu-id="c6b00-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="c6b00-349">Haga clic en una factoría de datos en el Explorador de servidores y seleccione **exportar factoría de datos tooNew proyecto** toocreate un proyecto de Visual Studio basado en un generador de datos existente.</span><span class="sxs-lookup"><span data-stu-id="c6b00-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Exportar el proyecto de VS de tooa de generador de datos](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="c6b00-351">Actualización de herramientas de Factoría de datos para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6b00-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="c6b00-352">Hola tooupdate herramientas de Data Factory de Azure para Visual Studio, siga los pasos:</span><span class="sxs-lookup"><span data-stu-id="c6b00-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="c6b00-353">Haga clic en **herramientas** en el menú de Hola y seleccione **extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="c6b00-354">Seleccione **actualizaciones** en Hola panel izquierdo y, a continuación, seleccione **Galería de Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="c6b00-355">Seleccione **Herramientas de Factoría de datos de Azure para Visual Studio** y haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="c6b00-356">Si no ve esta entrada, ya tiene la versión más reciente de Hola de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="c6b00-357">Uso de archivos de configuración</span><span class="sxs-lookup"><span data-stu-id="c6b00-357">Use configuration files</span></span>
<span data-ttu-id="c6b00-358">Puede usar archivos de configuración de propiedades de tooconfigure de Visual Studio para servicios/tablas/canalizaciones vinculadas diferente para cada entorno.</span><span class="sxs-lookup"><span data-stu-id="c6b00-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="c6b00-359">Considere la posibilidad de hello después de la definición de JSON para un servicio vinculado de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="c6b00-360">toospecify **connectionString** con valores diferentes para accountname y accountkey en función de hello entorno (desarrollo/prueba/producción) toowhich va a implementar las entidades de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="c6b00-361">Puede conseguir este comportamiento mediante el uso del archivo de configuración independiente para cada entorno.</span><span class="sxs-lookup"><span data-stu-id="c6b00-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="c6b00-362">Adición de un archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="c6b00-362">Add a configuration file</span></span>
<span data-ttu-id="c6b00-363">Agregue un archivo de configuración para cada entorno mediante la realización de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="c6b00-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="c6b00-364">Haga clic en proyecto de la factoría de datos de hello en la solución de Visual Studio, seleccione demasiado**agregar**y haga clic en **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="c6b00-365">Seleccione **Config** en hello lista de plantillas instaladas de hello izquierda, seleccione **archivo de configuración**, escriba un **nombre** para la configuración de Hola de archivo y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Adición de archivo de configuración](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="c6b00-367">Agregar parámetros de configuración y sus valores de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="c6b00-367">Add configuration parameters and their values in hello following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="c6b00-368">En este ejemplo se configura la propiedad connectionString de un servicio vinculado de Almacenamiento de Azure y un servicio vinculado de SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6b00-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="c6b00-369">Observe que la sintaxis de Hola para especificar el nombre es [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="c6b00-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="c6b00-370">Si JSON tiene una propiedad que tiene una matriz de valores como se muestra en el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c6b00-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="c6b00-371">Configure las propiedades como se muestra en hello (indización de base cero uso) el archivo de configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6b00-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="c6b00-372">Nombres de propiedad con espacios</span><span class="sxs-lookup"><span data-stu-id="c6b00-372">Property names with spaces</span></span>
<span data-ttu-id="c6b00-373">Si un nombre de propiedad contiene espacios, utilice corchetes como se muestra en el siguiente ejemplo (nombre de servidor de base de datos) de Hola:</span><span class="sxs-lookup"><span data-stu-id="c6b00-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="c6b00-374">Implementación de la solución mediante una configuración</span><span class="sxs-lookup"><span data-stu-id="c6b00-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="c6b00-375">Al publicar las entidades de la factoría de datos de Azure en VS, puede especificar configuración de Hola que desee toouse para esa operación de publicación.</span><span class="sxs-lookup"><span data-stu-id="c6b00-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="c6b00-376">entidades de toopublish en un proyecto de Data Factory de Azure mediante el archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="c6b00-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="c6b00-377">Haga clic en proyecto de la factoría de datos y haga clic en **publicar** toosee hello **publicar elementos** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="c6b00-378">Seleccione un generador de datos existente o especificar valores para la creación de una factoría de datos en hello **factoría de datos de configuración** página y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="c6b00-379">En hello **publicar elementos** página: verá una lista desplegable con las configuraciones disponibles para hello **Seleccionar configuración de implementación** campo.</span><span class="sxs-lookup"><span data-stu-id="c6b00-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Selección de archivo de configuración](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="c6b00-381">Seleccione hello **archivo de configuración** que haría como toouse y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="c6b00-382">Confirme que aparece el nombre de Hola de archivo JSON en hello **resumen** página y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6b00-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="c6b00-383">Haga clic en **finalizar** una vez finalizada la operación de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="c6b00-384">Cuando se implementa, valores de Hola Hola del archivo de configuración son tooset usa valores de propiedades en archivos JSON de hello antes de que las entidades de hello son tooAzure implementado el servicio de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="c6b00-385">Uso de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c6b00-385">Use Azure Key Vault</span></span>
<span data-ttu-id="c6b00-386">No es aconsejable y a menudo con la directiva toocommit datos confidenciales como repositorio de código de toohello de cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="c6b00-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="c6b00-387">Vea [seguros publicar ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) ejemplo en GitHub toolearn sobre cómo almacenar información confidencial en el almacén de claves de Azure y usarlo al publicar las entidades de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="c6b00-388">Hola seguros publicar la extensión para Visual Studio permite Hola secretos toobe almacenado en el almacén de claves y sólo toothem de referencias se especifican en los servicios vinculados / configuraciones de implementación.</span><span class="sxs-lookup"><span data-stu-id="c6b00-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="c6b00-389">Estas referencias se resuelven al publicar tooAzure de entidades de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="c6b00-390">Estos archivos se pueden confirmar toosource repositorio sin exponer los secretos.</span><span class="sxs-lookup"><span data-stu-id="c6b00-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6b00-391">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6b00-391">Next steps</span></span>
<span data-ttu-id="c6b00-392">En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="c6b00-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="c6b00-393">Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello:</span><span class="sxs-lookup"><span data-stu-id="c6b00-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="c6b00-394">toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6b00-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
