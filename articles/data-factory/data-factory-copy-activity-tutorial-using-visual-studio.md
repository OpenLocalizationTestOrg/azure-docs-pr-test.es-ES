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
ms.openlocfilehash: f90b158e45a3679210685765b23c8299eb76ed50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="09031-103">Tutorial: Crear una canalización con la actividad de copia mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09031-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09031-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="09031-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="09031-105">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="09031-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="09031-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="09031-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="09031-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09031-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="09031-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09031-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="09031-109">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="09031-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="09031-110">API DE REST</span><span class="sxs-lookup"><span data-stu-id="09031-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="09031-111">API de .NET</span><span class="sxs-lookup"><span data-stu-id="09031-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="09031-112">En este artículo, aprenderá a usar Microsoft Visual Studio para crear una factoría de datos con una canalización que copia datos desde Azure Blob Storage a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="09031-112">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="09031-113">Si no está familiarizado con Azure Data Factory, lea el artículo [Introducción a Azure Data Factory](data-factory-introduction.md) antes de realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="09031-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="09031-114">En este tutorial, creará una canalización con una actividad en ella: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="09031-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="09031-115">La actividad de copia realiza la copia de los datos de un almacén de datos admitido en un almacén de datos receptor.</span><span class="sxs-lookup"><span data-stu-id="09031-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="09031-116">Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="09031-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="09031-117">La actividad funciona con un servicio disponible de forma global que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="09031-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="09031-118">Para más información acerca de la actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="09031-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="09031-119">pero se puede tener más de una actividad en una canalización.</span><span class="sxs-lookup"><span data-stu-id="09031-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="09031-120">También puede encadenar dos actividades (ejecutar una después de otra) haciendo que el conjunto de datos de salida de una actividad sea el conjunto de datos de entrada de la otra actividad.</span><span class="sxs-lookup"><span data-stu-id="09031-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="09031-121">Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="09031-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="09031-122">La canalización de datos de este tutorial copia datos de un almacén de datos de origen a un almacén de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="09031-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="09031-123">Para ver un tutorial acerca de cómo transformar datos mediante Azure Data Factory, consulte [Tutorial: Compilación de la primera canalización para procesar datos mediante el clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="09031-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09031-124">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="09031-124">Prerequisites</span></span>
1. <span data-ttu-id="09031-125">Lea el artículo [Tutorial: Compilación de la primera canalización para procesar datos mediante el clúster de Hadoop](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) y complete los pasos de los **requisitos previos** .</span><span class="sxs-lookup"><span data-stu-id="09031-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span>       
2. <span data-ttu-id="09031-126">Para crear instancias de Data Factory, es preciso ser miembro del rol [Colaborador de Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) en el nivel de grupo de recursos o suscripción.</span><span class="sxs-lookup"><span data-stu-id="09031-126">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
3. <span data-ttu-id="09031-127">Debe tener lo siguiente instalado en el equipo:</span><span class="sxs-lookup"><span data-stu-id="09031-127">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="09031-128">Visual Studio 2013 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="09031-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="09031-129">Descargue el SDK de Azure para Visual Studio 2013 o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="09031-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="09031-130">Vaya a la [página Descargas de Azure](https://azure.microsoft.com/downloads/) y haga clic en **VS 2013** o **VS 2015** en la sección **.NET**.</span><span class="sxs-lookup"><span data-stu-id="09031-130">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="09031-131">Descargue el último complemento de Azure Data Factory para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="09031-131">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="09031-132">También puede actualizar el complemento, para lo que debe seguir estos pasos: en el menú, haga clic en **Herramientas** -> **Extensiones y actualizaciones** -> **En línea** -> **Galería de Visual Studio** -> **Herramientas de Factoría de datos de Microsoft Azure para Visual Studio** -> **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="09031-132">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="09031-133">Pasos</span><span class="sxs-lookup"><span data-stu-id="09031-133">Steps</span></span>
<span data-ttu-id="09031-134">Estos son los pasos que se realizan en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="09031-134">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="09031-135">Cree **servicios vinculados** en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-135">Create **linked services** in the data factory.</span></span> <span data-ttu-id="09031-136">En este paso, se crean dos servicios vinculados del tipo Azure Storage y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="09031-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="09031-137">AzureStorageLinkedService vincula una cuenta de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-137">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="09031-138">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó un contenedor y se cargaron datos en esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09031-138">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="09031-139">AzureSqlLinkedService vincula la base de datos SQL de Azure con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-139">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="09031-140">Los datos que se copian desde Blob Storage se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-140">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="09031-141">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó una tabla SQL en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="09031-142">Cree **conjuntos de datos** de entrada y salida en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-142">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="09031-143">El servicio vinculado Azure Storage especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="09031-143">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="09031-144">Además, el conjunto de datos de blobs de entrada especifica el contenedor y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="09031-144">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="09031-145">De forma similar, el servicio vinculado Azure SQL Database especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="09031-145">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="09031-146">Además, el conjunto de datos de la tabla SQL de salida especifica la tabla de la base de datos en la que se copian los datos de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="09031-146">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
3. <span data-ttu-id="09031-147">Cree una **canalización** en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-147">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="09031-148">En este paso, se crea una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="09031-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="09031-149">Esta actividad copia los datos desde un blob de Azure Blob Storage a una tabla de la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-149">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="09031-150">Puede utilizar una actividad de copia en una canalización para copiar datos desde cualquier origen admitido a cualquier destino admitido.</span><span class="sxs-lookup"><span data-stu-id="09031-150">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="09031-151">Para ver una lista de los almacenes de datos admitidos, consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="09031-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="09031-152">Cree una **factoría de datos** de Azure al implementar entidades de Data Factory (servicios vinculados, conjuntos de datos o tablas y canalizaciones).</span><span class="sxs-lookup"><span data-stu-id="09031-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="09031-153">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09031-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="09031-154">Inicie **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="09031-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="09031-155">Haga clic en **Archivo**, seleccione **Nuevo** y, luego, haga clic en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="09031-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="09031-156">Debería ver el cuadro de diálogo **Nuevo proyecto** .</span><span class="sxs-lookup"><span data-stu-id="09031-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="09031-157">En el cuadro de diálogo **Nuevo proyecto**, seleccione la plantilla **DataFactory** y haga clic en **Proyecto vacío de factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="09031-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Cuadro de diálogo Nuevo proyecto](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="09031-159">Especifique el nombre del proyecto, la ubicación y el nombre de la solución y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="09031-159">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span></span>
   
    ![Explorador de soluciones](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="09031-161">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="09031-161">Create linked services</span></span>
<span data-ttu-id="09031-162">Los servicios vinculados se crean en una factoría de datos para vincular los almacenes de datos y los servicios de proceso con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-162">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="09031-163">En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="09031-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="09031-164">Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino).</span><span class="sxs-lookup"><span data-stu-id="09031-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="09031-165">Por lo tanto, se crean dos servicios vinculados del tipo AzureStorage y AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="09031-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="09031-166">El servicio vinculado Azure Storage vincula una cuenta de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-166">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="09031-167">Esta cuenta de almacenamiento es la que se usó para crear un contenedor y con la que se cargaron los datos como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="09031-167">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="09031-168">Un servicio vinculado Azure SQL Database vincula una base de datos SQL de Azure con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-168">Azure SQL linked service links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="09031-169">Los datos que se copian desde Blob Storage se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-169">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="09031-170">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó la tabla emp en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-170">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="09031-171">Los servicios vinculados vinculan almacenes de datos o servicios de proceso con una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-171">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="09031-172">Consulte los [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver todos orígenes y receptores que admite la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="09031-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="09031-173">Consulte los [servicios vinculados de procesos](data-factory-compute-linked-services.md) para ver la lista de servicios de proceso compatibles con Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-173">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="09031-174">En este tutorial no se usan servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="09031-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="09031-175">Creación del servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="09031-175">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="09031-176">En el **Explorador de soluciones**, haga clic con el botón derecho en **Servicios vinculados**, seleccione **Agregar** y haga clic en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="09031-176">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="09031-177">En el cuadro de diálogo **Agregar nuevo elemento**, seleccione **Servicios vinculados de Almacenamiento de Azure** en la lista y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="09031-177">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![Nuevo servicio vinculado](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="09031-179">Reemplace `<accountname>` y `<accountkey>`* por el nombre de la cuenta de Azure Storage y su clave.</span><span class="sxs-lookup"><span data-stu-id="09031-179">Replace `<accountname>` and `<accountkey>`* with the name of your Azure storage account and its key.</span></span> 
   
    ![Servicio vinculado de Almacenamiento de Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="09031-181">Guarde el archivo **AzureStorageLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="09031-181">Save the **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="09031-182">Para más información sobre las propiedades JSON en la definición de servicio vinculado, vea el artículo [Conector de Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="09031-182">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="09031-183">Cree el servicio vinculado SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-183">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="09031-184">Haga doble clic con el botón derecho en el nodo **Servicios vinculados** en el **Explorador de soluciones** de nuevo, apunte a **Agregar** y haga clic en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="09031-184">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="09031-185">Esta vez, seleccione **Servicios vinculados de SQL Azure** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="09031-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="09031-186">En el archivo **AzureSqlLinkedService1.json**, reemplace `<servername>`, `<databasename>`, `<username@servername>` y `<password>` por los nombres del servidor, la base de datos, la cuenta de usuario y la contraseña de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-186">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="09031-187">Guarde el archivo **AzureSqlLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="09031-187">Save the **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="09031-188">Para más información acerca de estas propiedades JSON, consulte [Conector de Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="09031-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="09031-189">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="09031-189">Create datasets</span></span>
<span data-ttu-id="09031-190">En el paso anterior, creó servicios vinculados para vincular una cuenta de Azure Storage y una base de datos SQL de Azure con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-190">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="09031-191">En este paso, defina dos conjuntos de datos llamados InputDataset y OutputDataset, que representan los datos de entrada y salida que se almacenan en los almacenes de datos a los que hacen referencia AzureStorageLinkedService1 y AzureSqlLinkedService1, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="09031-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="09031-192">El servicio vinculado Azure Storage especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="09031-192">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="09031-193">Además, el conjunto de datos de blobs de entrada (InputDataset) especifica el contenedor y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="09031-193">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="09031-194">De forma similar, el servicio vinculado Azure SQL Database especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="09031-194">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="09031-195">Además, el conjunto de datos de la tabla SQL de salida (OutputDataset) especifica la tabla de la base de datos en la que se copian los datos de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="09031-195">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="09031-196">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="09031-196">Create input dataset</span></span>
<span data-ttu-id="09031-197">En este paso, se crea un conjunto de datos llamado InputDataset, que apunta a un archivo de blobs (emp.txt) en la carpeta raíz de un contenedor de blobs (adftutorial), en la instancia de Azure Storage representada por el servicio vinculado AzureStorageLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="09031-197">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="09031-198">Si no especifica un valor para fileName (o puede omitirlo), los datos de todos los blobs en la carpeta de entrada se copian en el destino.</span><span class="sxs-lookup"><span data-stu-id="09031-198">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="09031-199">En este tutorial, especifique un valor para fileName.</span><span class="sxs-lookup"><span data-stu-id="09031-199">In this tutorial, you specify a value for the fileName.</span></span> 

<span data-ttu-id="09031-200">Aquí, se usa el término "tablas" en lugar de "conjuntos de datos".</span><span class="sxs-lookup"><span data-stu-id="09031-200">Here, you use the term "tables" rather than "datasets".</span></span> <span data-ttu-id="09031-201">Una tabla es un conjunto de datos rectangular y es el único tipo de conjunto de datos que se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="09031-201">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="09031-202">Haga clic con el botón derecho en **Tablas** en el **Explorador de soluciones**, seleccione **Agregar** y haga clic en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="09031-202">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="09031-203">En el cuadro de diálogo **Agregar nuevo elemento**, seleccione **Blob de Azure** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="09031-203">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="09031-204">Reemplace el texto JSON con el texto siguiente y guarde el archivo **AzureBlobLocation1.json** .</span><span class="sxs-lookup"><span data-stu-id="09031-204">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

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
    <span data-ttu-id="09031-205">En la siguiente tabla se ofrecen descripciones de las propiedades JSON que se usan en el fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="09031-205">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="09031-206">Propiedad</span><span class="sxs-lookup"><span data-stu-id="09031-206">Property</span></span> | <span data-ttu-id="09031-207">Descripción</span><span class="sxs-lookup"><span data-stu-id="09031-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="09031-208">type</span><span class="sxs-lookup"><span data-stu-id="09031-208">type</span></span> | <span data-ttu-id="09031-209">La propiedad type se establece en **AzureBlob** porque los datos residen en una instancia de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="09031-209">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="09031-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="09031-210">linkedServiceName</span></span> | <span data-ttu-id="09031-211">Hace referencia al servicio **AzureStorageLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="09031-211">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="09031-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="09031-212">folderPath</span></span> | <span data-ttu-id="09031-213">Especifica el **contenedor** de blobs y la **carpeta** que contiene los blobs de entrada.</span><span class="sxs-lookup"><span data-stu-id="09031-213">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="09031-214">En este tutorial, adftutorial es el contenedor de blobs y folder es la carpeta raíz.</span><span class="sxs-lookup"><span data-stu-id="09031-214">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="09031-215">fileName</span><span class="sxs-lookup"><span data-stu-id="09031-215">fileName</span></span> | <span data-ttu-id="09031-216">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="09031-216">This property is optional.</span></span> <span data-ttu-id="09031-217">Si omite esta propiedad, se seleccionan todos los archivos de folderPath.</span><span class="sxs-lookup"><span data-stu-id="09031-217">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="09031-218">En este tutorial, se especifica **emp.txt** en fileName, por lo que solo se selecciona ese archivo para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="09031-218">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="09031-219">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="09031-219">format -> type</span></span> |<span data-ttu-id="09031-220">El archivo de entrada tiene formato de texto, por lo que usamos **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="09031-220">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="09031-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="09031-221">columnDelimiter</span></span> | <span data-ttu-id="09031-222">Las columnas del archivo de entrada están delimitadas por **coma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="09031-222">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="09031-223">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="09031-223">frequency/interval</span></span> | <span data-ttu-id="09031-224">La frecuencia está establecida en **Hour** y el intervalo es **1**, lo que significa que los segmentos de entrada estarán disponibles **cada hora**.</span><span class="sxs-lookup"><span data-stu-id="09031-224">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="09031-225">En otras palabras, el servicio Data Factory busca los datos de entrada cada hora en la carpeta raíz del contenedor de blobs (**adftutorial**) que se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="09031-225">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="09031-226">Busca los datos entre las horas de inicio y finalización de la canalización, no antes ni después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="09031-226">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="09031-227">external</span><span class="sxs-lookup"><span data-stu-id="09031-227">external</span></span> | <span data-ttu-id="09031-228">Esta propiedad se establece en **true** si esta canalización no ha generado los datos.</span><span class="sxs-lookup"><span data-stu-id="09031-228">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="09031-229">Los datos de entrada de este tutorial están en el archivo emp.txt, que no lo generó esta canalización, por lo que establecemos esta propiedad en true.</span><span class="sxs-lookup"><span data-stu-id="09031-229">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="09031-230">Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="09031-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="09031-231">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="09031-231">Create output dataset</span></span>
<span data-ttu-id="09031-232">En este paso se crea un conjunto de datos de salida denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="09031-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="09031-233">Este conjunto de datos apunta a una tabla SQL de Azure SQL Database representada por **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="09031-233">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="09031-234">Haga clic con el botón derecho en **Tablas** en el **Explorador de soluciones** de nuevo, seleccione **Agregar** y haga clic en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="09031-234">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="09031-235">En el cuadro de diálogo **Agregar nuevo elemento**, seleccione **SQL de Azure** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="09031-235">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="09031-236">Reemplace el texto JSON con el JSON siguiente y guarde el archivo **AzureSqlTableLocation1.json** .</span><span class="sxs-lookup"><span data-stu-id="09031-236">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

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
    <span data-ttu-id="09031-237">En la siguiente tabla se ofrecen descripciones de las propiedades JSON que se usan en el fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="09031-237">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="09031-238">Propiedad</span><span class="sxs-lookup"><span data-stu-id="09031-238">Property</span></span> | <span data-ttu-id="09031-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="09031-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="09031-240">type</span><span class="sxs-lookup"><span data-stu-id="09031-240">type</span></span> | <span data-ttu-id="09031-241">La propiedad type se establece en **AzureSqlTable** porque los datos se copian en una tabla de una base de datos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="09031-241">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="09031-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="09031-242">linkedServiceName</span></span> | <span data-ttu-id="09031-243">Hace referencia al servicio **AzureSqlLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="09031-243">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="09031-244">tableName</span><span class="sxs-lookup"><span data-stu-id="09031-244">tableName</span></span> | <span data-ttu-id="09031-245">Especifica la **tabla** en la que se copian los datos.</span><span class="sxs-lookup"><span data-stu-id="09031-245">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="09031-246">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="09031-246">frequency/interval</span></span> | <span data-ttu-id="09031-247">La frecuencia se establece en **Hour** y el intervalo es **1**, lo que significa que los sectores de salida se producen **cada hora** entre las horas de inicio y finalización de la canalización, no antes ni después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="09031-247">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="09031-248">En la tabla emp de la base de datos hay tres columnas: **ID**, **FirstName** y **LastName**.</span><span class="sxs-lookup"><span data-stu-id="09031-248">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="09031-249">ID es una columna de identidad, por lo que deberá especificar solo **FirstName** y **LastName** aquí.</span><span class="sxs-lookup"><span data-stu-id="09031-249">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="09031-250">Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="09031-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="09031-251">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="09031-251">Create pipeline</span></span>
<span data-ttu-id="09031-252">En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="09031-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="09031-253">Actualmente, el conjunto de datos de salida es lo que impulsa la programación.</span><span class="sxs-lookup"><span data-stu-id="09031-253">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="09031-254">En este tutorial, el conjunto de datos de salida está configurado para generar un segmento una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="09031-254">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="09031-255">La canalización tiene una hora de inicio y una hora de finalización con un día de diferencia, es decir, 24 horas.</span><span class="sxs-lookup"><span data-stu-id="09031-255">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="09031-256">Por lo tanto, la canalización produce 24 segmentos del conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="09031-256">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="09031-257">Haga clic con el botón derecho en **Canalizaciones** en el **Explorador de soluciones**, seleccione **Agregar** y haga clic en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="09031-257">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="09031-258">Seleccione **Copiar canalización de datos** en el cuadro de diálogo **Agregar nuevo elemento** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="09031-258">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="09031-259">Reemplace el JSON por el siguiente JSON y guarde el archivo **CopyActivity1.json** .</span><span class="sxs-lookup"><span data-stu-id="09031-259">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob to Azure SQL table",
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
    - <span data-ttu-id="09031-260">En la sección de actividades, solo hay una actividad con **type** establecido en **Copy**.</span><span class="sxs-lookup"><span data-stu-id="09031-260">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="09031-261">Para más información acerca de la actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="09031-261">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="09031-262">En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="09031-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="09031-263">La entrada de la actividad está establecida en **InputDataset**, mientras que la salida está establecida en **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="09031-263">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="09031-264">En la sección **typeProperties**, **BlobSource** se especifica como el tipo de origen y **SqlSink** como el tipo de receptor.</span><span class="sxs-lookup"><span data-stu-id="09031-264">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="09031-265">Consulte la lista de [almacenes de datos que se admiten](data-factory-data-movement-activities.md#supported-data-stores-and-formats) como orígenes y receptores de la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="09031-265">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="09031-266">Para más información sobre cómo usar un almacén de datos admitido específico como receptor de origen, haga clic en el vínculo en la tabla.</span><span class="sxs-lookup"><span data-stu-id="09031-266">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="09031-267">Reemplace el valor de la propiedad **start** por el día actual y el valor **end** por el próximo día.</span><span class="sxs-lookup"><span data-stu-id="09031-267">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="09031-268">Puede especificar solo la parte de fecha y omitir la parte de hora de la fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="09031-268">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="09031-269">Por ejemplo, "03-02-2016", que es equivalente a "03-02-2016T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="09031-269">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="09031-270">Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="09031-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="09031-271">Por ejemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="09031-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="09031-272">La hora de finalización ( **end** ) es opcional, pero se utilizará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="09031-272">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="09031-273">Si no especifica ningún valor para la propiedad **end**, se calcula como "**start + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="09031-273">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="09031-274">Para ejecutar la canalización indefinidamente, especifique **9999-09-09** como valor de propiedad **end**.</span><span class="sxs-lookup"><span data-stu-id="09031-274">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="09031-275">En el ejemplo anterior hay 24 segmentos de datos, ya que cada segmento de datos se produce cada hora.</span><span class="sxs-lookup"><span data-stu-id="09031-275">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="09031-276">Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="09031-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="09031-277">Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="09031-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="09031-278">Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="09031-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="09031-279">Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="09031-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="09031-280">Publicación e implementación de las entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="09031-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="09031-281">En este paso, se publican las entidades de Data Factory (servicios vinculados, conjuntos de datos y canalización) que se crearon anteriormente.</span><span class="sxs-lookup"><span data-stu-id="09031-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="09031-282">También se especifica el nombre de la nueva instancia de Data Factory que se va a crear para almacenar dichas entidades.</span><span class="sxs-lookup"><span data-stu-id="09031-282">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="09031-283">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="09031-283">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="09031-284">Si ve el cuadro de diálogo **Iniciar sesión en tu cuenta Microsoft**, escriba sus credenciales para la cuenta que tiene la suscripción de Azure y haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="09031-284">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="09031-285">Debería ver el siguiente cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="09031-285">You should see the following dialog box:</span></span>
   
   ![Cuadro de diálogo Publicar](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="09031-287">En la página Configure data factory (Configurar Data Factory), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="09031-287">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="09031-288">Seleccione la opción **Crear la nueva factoría de datos** .</span><span class="sxs-lookup"><span data-stu-id="09031-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="09031-289">Escriba **VSTutorialFactory** para **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="09031-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="09031-290">El nombre del generador de datos de Azure debe ser único global.</span><span class="sxs-lookup"><span data-stu-id="09031-290">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="09031-291">Si recibe un error sobre el nombre de la factoría de datos cuando se publica, cámbielo (por ejemplo, sunombreVSTutorialFactory) e intente publicar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="09031-291">If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="09031-292">Consulte el tema [Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para conocer las reglas de nomenclatura para los artefactos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="09031-293">Seleccione su suscripción de Azure en el campo **Suscripción** .</span><span class="sxs-lookup"><span data-stu-id="09031-293">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="09031-294">Si no ve ninguna suscripción, asegúrese de que ha iniciado sesión con una cuenta que sea administrador o coadministrador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="09031-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="09031-295">Seleccione el **grupo de recursos** para la factoría de datos que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="09031-295">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="09031-296">Seleccione la **Región** de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-296">Select the **region** for the data factory.</span></span> <span data-ttu-id="09031-297">La lista desplegable solo muestra las regiones que admite el servicio Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-297">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="09031-298">Haga clic en **Siguiente** para cambiar a la página **Publicar elementos**.</span><span class="sxs-lookup"><span data-stu-id="09031-298">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![Configurar página de Data Factory](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="09031-300">En la página **Publicar elementos**, asegúrese de que todas las factorías de datos están seleccionadas y haga clic en **Siguiente** para cambiar a la página **Resumen**.</span><span class="sxs-lookup"><span data-stu-id="09031-300">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![Página Publicar elementos](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="09031-302">Revise el resumen y haga clic en **Siguiente** para iniciar el proceso de implementación y ver el **Estado de implementación**.</span><span class="sxs-lookup"><span data-stu-id="09031-302">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![Página Publicar resumen](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="09031-304">En la página **Estado de implementación** , debería ver el estado del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="09031-304">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="09031-305">Cuando se haya completado la implementación, haga clic en Finalizar.</span><span class="sxs-lookup"><span data-stu-id="09031-305">Click Finish after the deployment is done.</span></span>
 
   ![Página Estado de la implementación](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="09031-307">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="09031-307">Note the following points:</span></span> 

* <span data-ttu-id="09031-308">Si recibe el error: "La suscripción no está registrada para usar el espacio de nombres Microsoft.DataFactory", realice una de las acciones siguientes e intente publicarla de nuevo:</span><span class="sxs-lookup"><span data-stu-id="09031-308">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="09031-309">En Azure PowerShell, ejecute el siguiente comando para registrar el proveedor de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-309">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="09031-310">Puede ejecutar el comando siguiente para confirmar que se ha registrado el proveedor de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-310">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="09031-311">Inicie sesión mediante la suscripción de Azure en el [Portal de Azure](https://portal.azure.com) y vaya a una hoja de Data Factory (o) cree una factoría de datos en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-311">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="09031-312">Esta acción registra automáticamente el proveedor.</span><span class="sxs-lookup"><span data-stu-id="09031-312">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="09031-313">El nombre de la factoría de datos se puede registrar como un nombre DNS en el futuro y, por lo tanto, hacerse públicamente visible.</span><span class="sxs-lookup"><span data-stu-id="09031-313">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09031-314">Para crear instancias de Data Factory, es preciso ser administrador o coadministrador de la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="09031-314">To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="09031-315">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="09031-315">Monitor pipeline</span></span>
<span data-ttu-id="09031-316">Vaya a la página principal de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="09031-316">Navigate to the home page for your data factory:</span></span>

1. <span data-ttu-id="09031-317">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09031-317">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="09031-318">En el menú izquierdo, haga clic en **Más servicios** y en **Factorías de datos**.</span><span class="sxs-lookup"><span data-stu-id="09031-318">Click **More services** on the left menu, and click **Data factories**.</span></span>

    ![Examinar factorías de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="09031-320">Comience a escribir el nombre de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-320">Start typing the name of your data factory.</span></span>

    ![Nombre de la factoría de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="09031-322">Haga clic en la factoría de datos en la lista de resultados para ver la página principal de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="09031-322">Click your data factory in the results list to see the home page for your data factory.</span></span>

    ![Página principal de Factoría de datos](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="09031-324">Siga las instrucciones que se indican en [Supervisión de conjuntos de datos y canalizaciones](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) para supervisar la canalización y los conjuntos de datos que ha creado en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="09031-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="09031-325">Actualmente, Visual Studio no permite supervisar canalizaciones de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="09031-326">Resumen</span><span class="sxs-lookup"><span data-stu-id="09031-326">Summary</span></span>
<span data-ttu-id="09031-327">En este tutorial, ha creado una factoría de datos de Azure para copiar datos de un blob de Azure en una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-327">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="09031-328">Ha usado Visual Studio para crear la factoría de datos, los servicios vinculados, los conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="09031-328">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="09031-329">Estos son los pasos de alto nivel que realizó en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="09031-329">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="09031-330">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="09031-331">Ha creado **servicios vinculados**.</span><span class="sxs-lookup"><span data-stu-id="09031-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="09031-332">Un servicio vinculado **Almacenamiento de Azure** para vincular la cuenta de almacenamiento de Azure que contiene datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="09031-332">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="09031-333">Un servicio vinculado **SQL Azure** para vincular la base de datos SQL de Azure que contiene los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="09031-333">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="09031-334">Ha creado **conjuntos de datos**que describen los datos de entrada y salida para las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="09031-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="09031-335">Ha creado una **canalización** con una **actividad de copia** con un origen **BlobSource** y un receptor **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="09031-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="09031-336">Para ver un tutorial acerca de cómo usar una actividad de Hive en HDInsight para transformar datos mediante un clúster de Azure HDInsight, consulte [Tutorial: Compilación de la primera canalización para transformar datos mediante el clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="09031-336">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="09031-337">Puede encadenar dos actividades (ejecutar una después de otra) haciendo que el conjunto de datos de salida de una actividad sea el conjunto de datos de entrada de la otra actividad.</span><span class="sxs-lookup"><span data-stu-id="09031-337">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="09031-338">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="09031-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="09031-339">Presentación de todas las factorías de datos en el explorador de servidores</span><span class="sxs-lookup"><span data-stu-id="09031-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="09031-340">En esta sección se describe cómo usar el explorador de servidores de Visual Studio para ver todas las factorías de datos de su suscripción de Azure, y cómo crear un proyecto de Visual Studio basado en una factoría de datos existente.</span><span class="sxs-lookup"><span data-stu-id="09031-340">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="09031-341">En **Visual Studio** haga clic en **Vista** en el menú y haga clic en **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="09031-341">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="09031-342">En la ventana Explorador de servidores, expanda **Azure** y **Factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="09031-342">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="09031-343">Si aparece **Iniciar sesión en Visual Studio**, escriba la **cuenta** asociada a su suscripción de Azure y haga clic en **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="09031-343">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="09031-344">Escriba la **contraseña** y haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="09031-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="09031-345">Visual Studio intenta obtener información acerca de todas las factorías de datos de Azure de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="09031-345">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="09031-346">Puede ver el estado de esta operación en la ventana **Data Factory Task List** (Lista de tareas de Data Factory).</span><span class="sxs-lookup"><span data-stu-id="09031-346">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Explorador de servidores](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="09031-348">Creación de un proyecto de Visual Studio para una factoría de datos existente</span><span class="sxs-lookup"><span data-stu-id="09031-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="09031-349">Haga clic con el botón derecho en una factoría de datos en el Explorador de servidores y seleccione **Exportar factoría de datos al nuevo proyecto** para crear un proyecto de Visual Studio basado en una factoría de datos existente.</span><span class="sxs-lookup"><span data-stu-id="09031-349">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Exportar factoría de datos a un proyecto de VS](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="09031-351">Actualización de herramientas de Factoría de datos para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09031-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="09031-352">Para actualizar las herramientas de Azure Data Factory para Visual Studio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="09031-352">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="09031-353">Haga clic en el menú **Herramientas** y seleccione **Extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="09031-353">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="09031-354">Seleccione **Actualizaciones** en el panel izquierdo y, luego, seleccione **Galería de Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="09031-354">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="09031-355">Seleccione **Herramientas de Factoría de datos de Azure para Visual Studio** y haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="09031-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="09031-356">Si no ve esta entrada, ya tiene la versión más reciente de las herramientas.</span><span class="sxs-lookup"><span data-stu-id="09031-356">If you do not see this entry, you already have the latest version of the tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="09031-357">Uso de archivos de configuración</span><span class="sxs-lookup"><span data-stu-id="09031-357">Use configuration files</span></span>
<span data-ttu-id="09031-358">Puede usar archivos de configuración de Visual Studio para configurar propiedades para servicios vinculados/tablas/canalizaciones distintos para cada entorno.</span><span class="sxs-lookup"><span data-stu-id="09031-358">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="09031-359">Considere la siguiente definición de JSON para un servicio vinculado de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-359">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="09031-360">Con ella, podrá especificar la propiedad **connectionString** con distintos valores para accountname y accountkey basados en el entorno (desarrollo, pruebas y producción) en el que va a implementar las entidades de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-360">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="09031-361">Puede conseguir este comportamiento mediante el uso del archivo de configuración independiente para cada entorno.</span><span class="sxs-lookup"><span data-stu-id="09031-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="09031-362">Adición de un archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="09031-362">Add a configuration file</span></span>
<span data-ttu-id="09031-363">Agregue un archivo de configuración a cada entorno realizando los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="09031-363">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="09031-364">En la solución de Visual Studio, haga clic con el botón derecho en el proyecto de Data Factory, seleccione **Agregar** y haga clic en **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="09031-364">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="09031-365">Seleccione **Config** en la lista de plantillas instaladas que encontrará a la izquierda, elija **Archivo de configuración**, especifique un **nombre** para este archivo y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="09031-365">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Adición de archivo de configuración](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="09031-367">Agregue parámetros de configuración y sus valores en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="09031-367">Add configuration parameters and their values in the following format:</span></span>

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

    <span data-ttu-id="09031-368">En este ejemplo se configura la propiedad connectionString de un servicio vinculado de Almacenamiento de Azure y un servicio vinculado de SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="09031-369">Observe que la sintaxis para especificar el nombre es [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="09031-369">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="09031-370">Si JSON tiene una propiedad con una matriz de valores como se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="09031-370">If JSON has a property that has an array of values as shown in the following code:</span></span>  

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

    <span data-ttu-id="09031-371">Configure las propiedades tal como se muestra en el siguiente archivo de configuración (use la indexación de base cero):</span><span class="sxs-lookup"><span data-stu-id="09031-371">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="09031-372">Nombres de propiedad con espacios</span><span class="sxs-lookup"><span data-stu-id="09031-372">Property names with spaces</span></span>
<span data-ttu-id="09031-373">Si un nombre de propiedad contiene espacios, utilice corchetes como se muestra en el ejemplo siguiente (nombre de servidor de base de datos):</span><span class="sxs-lookup"><span data-stu-id="09031-373">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="09031-374">Implementación de la solución mediante una configuración</span><span class="sxs-lookup"><span data-stu-id="09031-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="09031-375">Al publicar las entidades de Factoría de datos de Azure en Visual Studio, puede especificar la configuración que desea usar para esa operación de publicación.</span><span class="sxs-lookup"><span data-stu-id="09031-375">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="09031-376">Para publicar entidades en un proyecto de Factoría de datos de Azure mediante el archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="09031-376">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="09031-377">Haga clic con el botón derecho en el proyecto de Data Factory y después haga clic en **Publicar** para abrir el cuadro de diálogo **Publish Items** (Publicar elementos).</span><span class="sxs-lookup"><span data-stu-id="09031-377">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="09031-378">Seleccione una factoría de datos existente o especifique los valores necesarios para crear una en la página **Configure data factory** (Configurar Data Factory) y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="09031-378">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="09031-379">En la página **Publish Items** (Publicar elementos), verá una lista desplegable con las configuraciones disponibles para el campo **Select Deployment Config** (Seleccionar configuración de implementación).</span><span class="sxs-lookup"><span data-stu-id="09031-379">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Selección de archivo de configuración](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="09031-381">Seleccione el **archivo de configuración** que desea usar y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="09031-381">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="09031-382">Confirme que ve el nombre del archivo JSON en la página **Resumen** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="09031-382">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="09031-383">Cuando finalice la operación de implementación, haga clic en **Finalizar** .</span><span class="sxs-lookup"><span data-stu-id="09031-383">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="09031-384">Cuando realiza la implementación, se usan los valores del archivo de configuración para establecer los valores de las propiedades de los archivos JSON antes de que las entidades se implementen en el servicio Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-384">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="09031-385">Uso de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="09031-385">Use Azure Key Vault</span></span>
<span data-ttu-id="09031-386">No es aconsejable y, en ocasiones, contraviene la directiva de seguridad, confirmar información confidencial, como las cadenas de conexión, en el repositorio de código.</span><span class="sxs-lookup"><span data-stu-id="09031-386">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="09031-387">Vea el ejemplo [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) en GitHub para obtener información sobre cómo almacenar información confidencial en Azure Key Vault y usarla al publicar entidades de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="09031-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="09031-388">La extensión Secure Publish de Visual Studio permite almacenar los secretos en Key Vault, y solo las referencias a ellos se especifican en las configuraciones de implementación o en los servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="09031-388">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="09031-389">Estas referencias se resuelven al publicar las entidades de Data Factory en Azure.</span><span class="sxs-lookup"><span data-stu-id="09031-389">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="09031-390">Estos archivos se pueden confirmar en el repositorio de origen sin exponer los secretos.</span><span class="sxs-lookup"><span data-stu-id="09031-390">These files can then be committed to source repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="09031-391">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09031-391">Next steps</span></span>
<span data-ttu-id="09031-392">En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="09031-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="09031-393">En la tabla siguiente se proporciona una lista de almacenes de datos que se admiten como orígenes y destinos de la actividad de copia:</span><span class="sxs-lookup"><span data-stu-id="09031-393">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="09031-394">Para aprender a copiar datos hacia y desde un almacén de datos, haga clic en el vínculo del almacén de datos en la tabla.</span><span class="sxs-lookup"><span data-stu-id="09031-394">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>