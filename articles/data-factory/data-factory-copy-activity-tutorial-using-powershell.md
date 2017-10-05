---
title: "Tutorial: Creación de una canalización con la actividad de copia para mover datos con Azure PowerShell | Microsoft Docs"
description: "En este tutorial, creará una canalización de Azure Data Factory con una actividad de copia mediante Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 81efe7c6af29af778686e1f6bcf62fedc9711052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="fd2fe-103">Tutorial: Creación de una canalización de Data Factory para mover datos mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd2fe-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd2fe-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd2fe-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="fd2fe-105">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="fd2fe-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="fd2fe-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fd2fe-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="fd2fe-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd2fe-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="fd2fe-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd2fe-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="fd2fe-109">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd2fe-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="fd2fe-110">API DE REST</span><span class="sxs-lookup"><span data-stu-id="fd2fe-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="fd2fe-111">API de .NET</span><span class="sxs-lookup"><span data-stu-id="fd2fe-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="fd2fe-112">En este artículo, aprenderá a usar PowerShell para crear una factoría de datos con una canalización que copia datos desde un almacén de Azure Blob Storage en una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-112">In this article, you learn how to use PowerShell to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="fd2fe-113">Si no está familiarizado con Azure Data Factory, lea el artículo [Introducción a Azure Data Factory](data-factory-introduction.md) antes de realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="fd2fe-114">En este tutorial, creará una canalización con una actividad en ella: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="fd2fe-115">La actividad de copia realiza la copia de los datos de un almacén de datos admitido en un almacén de datos receptor.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="fd2fe-116">Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fd2fe-117">La actividad funciona con un servicio disponible de forma global que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="fd2fe-118">Para más información acerca de la actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="fd2fe-119">pero se puede tener más de una actividad en una canalización.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="fd2fe-120">También puede encadenar dos actividades (ejecutar una después de otra) haciendo que el conjunto de datos de salida de una actividad sea el conjunto de datos de entrada de la otra actividad.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="fd2fe-121">Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="fd2fe-122">Este artículo no abarca todos los cmdlets de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-122">This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="fd2fe-123">Vea [Referencia de cmdlets de Data Factory](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre estos cmdlets.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="fd2fe-124">La canalización de datos de este tutorial copia datos de un almacén de datos de origen a un almacén de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="fd2fe-125">Para ver un tutorial acerca de cómo transformar datos mediante Azure Data Factory, consulte [Tutorial: Compilación de la primera canalización para procesar datos mediante el clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd2fe-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd2fe-126">Prerequisites</span></span>
- <span data-ttu-id="fd2fe-127">Complete los [requisitos previos del tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-127">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="fd2fe-128">Instale **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="fd2fe-129">Siga las instrucciones de [Instalación y configuración de Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-129">Follow the instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="fd2fe-130">Pasos</span><span class="sxs-lookup"><span data-stu-id="fd2fe-130">Steps</span></span>
<span data-ttu-id="fd2fe-131">Estos son los pasos que se realizan en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-131">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="fd2fe-132">Cree una **factoría de datos** de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="fd2fe-133">En este paso, creará una factoría de datos llamada ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="fd2fe-134">Cree **servicios vinculados** en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-134">Create **linked services** in the data factory.</span></span> <span data-ttu-id="fd2fe-135">En este paso, se crean dos servicios vinculados del tipo Azure Storage y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="fd2fe-136">AzureStorageLinkedService vincula una cuenta de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-136">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="fd2fe-137">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó un contenedor y se cargaron datos en esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-137">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="fd2fe-138">AzureSqlLinkedService vincula la base de datos SQL de Azure con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-138">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="fd2fe-139">Los datos que se copian desde Blob Storage se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-139">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="fd2fe-140">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó una tabla SQL en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="fd2fe-141">Cree **conjuntos de datos** de entrada y salida en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-141">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="fd2fe-142">El servicio vinculado Azure Storage especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-142">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="fd2fe-143">Además, el conjunto de datos de blobs de entrada especifica el contenedor y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-143">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="fd2fe-144">De forma similar, el servicio vinculado Azure SQL Database especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-144">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="fd2fe-145">Además, el conjunto de datos de la tabla SQL de salida especifica la tabla de la base de datos en la que se copian los datos de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-145">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="fd2fe-146">Cree una **canalización** en la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-146">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="fd2fe-147">En este paso, se crea una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="fd2fe-148">Esta actividad copia los datos desde un blob de Azure Blob Storage a una tabla de la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-148">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="fd2fe-149">Puede utilizar una actividad de copia en una canalización para copiar datos desde cualquier origen admitido a cualquier destino admitido.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-149">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="fd2fe-150">Para ver una lista de los almacenes de datos admitidos, consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="fd2fe-151">Supervise la canalización.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-151">Monitor the pipeline.</span></span> <span data-ttu-id="fd2fe-152">En este paso, **supervisará** los segmentos de los conjuntos de datos de entrada y salida con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-152">In this step, you **monitor** the slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="fd2fe-153">Crear una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="fd2fe-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fd2fe-154">Complete los [requisitos previos del tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-154">Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="fd2fe-155">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="fd2fe-156">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="fd2fe-157">Por ejemplo, una actividad de copia para copiar datos desde un origen a un almacén de datos de destino o una actividad de Hive de HDInsight para ejecutar un script de Hive que transforme los datos de entrada para generar datos de salida.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-157">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="fd2fe-158">Comencemos con la creación de la factoría de datos en este paso.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-158">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="fd2fe-159">Inicie **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-159">Launch **PowerShell**.</span></span> <span data-ttu-id="fd2fe-160">Mantenga Azure PowerShell abierto hasta el final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-160">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="fd2fe-161">Si lo cierra y vuelve a abrirlo, deberá ejecutar los comandos de nuevo.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-161">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="fd2fe-162">Ejecute el siguiente comando y escriba el nombre de usuario y la contraseña que utiliza para iniciar sesión en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-162">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="fd2fe-163">Ejecute el siguiente comando para ver todas las suscripciones de esta cuenta:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-163">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="fd2fe-164">Ejecute el comando siguiente para seleccionar la suscripción con la que desea trabajar.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-164">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="fd2fe-165">Reemplace **&lt;NameOfAzureSubscription**&gt; por el nombre de su suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-165">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="fd2fe-166">Cree un grupo de recursos de Azure con el nombre: **ADFTutorialResourceGroup** mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="fd2fe-167">En algunos de los pasos de este tutorial se supone que se usa el grupo de recursos denominado **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-167">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="fd2fe-168">Si usa un otro grupo de recursos, deberá usarlo en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-168">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="fd2fe-169">Ejecute el cmdlet **New-AzureRmDataFactory** para crear una instancia de Data Factory denominada **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-169">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="fd2fe-170">Puede que ya se esté usando este nombre.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-170">This name may already have been taken.</span></span> <span data-ttu-id="fd2fe-171">Para que el nombre de la factoría de datos sea único, agregue un prefijo o un sufijo (por ejemplo: ADFTutorialDataFactoryPSH05152017) y vuelva a ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-171">Therefore, make the name of the data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run the command again.</span></span>  

<span data-ttu-id="fd2fe-172">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-172">Note the following points:</span></span>

* <span data-ttu-id="fd2fe-173">El nombre del generador de datos de Azure debe ser único global.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-173">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="fd2fe-174">Si recibe el siguiente error, cambie el nombre (por ejemplo, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-174">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="fd2fe-175">Use este nombre en lugar de ADFTutorialFactoryPSH mientras lleva a cabo los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="fd2fe-176">Consulte [Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="fd2fe-177">Para crear instancias de Data Factory, debe ser administrador o colaborador en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-177">To create Data Factory instances, you must be a contributor or administrator of the Azure subscription.</span></span>
* <span data-ttu-id="fd2fe-178">El nombre de la factoría de datos se puede registrar como un nombre DNS en el futuro y, por lo tanto, que sea visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-178">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span></span>
* <span data-ttu-id="fd2fe-179">Es posible que reciba el siguiente error: "**La suscripción no está registrada para usar el espacio de nombres Microsoft.DataFactory**".</span><span class="sxs-lookup"><span data-stu-id="fd2fe-179">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="fd2fe-180">Realice una de las siguientes acciones e intente publicar de nuevo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-180">Do one of the following, and try publishing again:</span></span>

  * <span data-ttu-id="fd2fe-181">En Azure PowerShell, ejecute el siguiente comando para registrar el proveedor de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-181">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="fd2fe-182">Ejecute el comando siguiente para confirmar que se ha registrado el proveedor de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-182">Run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="fd2fe-183">Inicie sesión en [Azure Portal](https://portal.azure.com) mediante la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-183">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fd2fe-184">Vaya a una hoja de Data Factory o cree una instancia de Data Factory en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-184">Go to a Data Factory blade, or create a data factory in the Azure portal.</span></span> <span data-ttu-id="fd2fe-185">Esta acción registra automáticamente el proveedor.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-185">This action automatically registers the provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="fd2fe-186">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="fd2fe-186">Create linked services</span></span>
<span data-ttu-id="fd2fe-187">Los servicios vinculados se crean en una factoría de datos para vincular los almacenes de datos y los servicios de proceso con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-187">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="fd2fe-188">En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="fd2fe-189">Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="fd2fe-190">Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="fd2fe-191">AzureStorageLinkedService vincula una cuenta de Azure Storage a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-191">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="fd2fe-192">Esta cuenta de almacenamiento es la que se usó para crear un contenedor y con la que se cargaron los datos como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-192">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="fd2fe-193">AzureSqlLinkedService vincula la base de datos SQL de Azure con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-193">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="fd2fe-194">Los datos que se copian desde Blob Storage se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-194">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="fd2fe-195">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó la tabla emp en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-195">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="fd2fe-196">Creación de un servicio vinculado para una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="fd2fe-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="fd2fe-197">En este paso, vinculará su cuenta de Azure Storage con su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-197">In this step, you link your Azure storage account to your data factory.</span></span>

1. <span data-ttu-id="fd2fe-198">Cree un archivo JSON llamado **AzureStorageLinkedService.json** en la carpeta **C:\ADFGetStartedPSH** con el siguiente contenido: (cree la carpeta ADFGetStartedPSH si aún no existe).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with the following content: (Create the folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fd2fe-199">Reemplace &lt;accountname&gt; y &lt;accountkey&gt; por el nombre y la clave de su cuenta de Azure Storage antes de guardar el archivo.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving the file.</span></span> 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. <span data-ttu-id="fd2fe-200">En **Azure PowerShell**, cambie a la carpeta **ADFGetStartedPSH**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-200">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="fd2fe-201">Ejecute el cmdlet **New-AzureRmDataFactoryLinkedService** para crear el servicio vinculado: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-201">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="fd2fe-202">Tanto el cmdlet como otros cmdlets de Data Factory que se usan en este tutorial requieren que se pasen los valores de los parámetros **ResourceGroupName** y **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="fd2fe-203">Como alternativa, puede pasar el objeto DataFactory devuelto por el cmdlet New-AzureRmDataFactory sin escribir ResourceGroupName y DataFactoryName cada vez que ejecute un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-203">Alternatively, you can pass the DataFactory object returned by the New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="fd2fe-204">Este es la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-204">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="fd2fe-205">Otra manera de crear este servicio vinculado es especificar el nombre del grupo de recursos y el nombre de la factoría de datos en lugar de especificar el objeto DataFactory.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-205">Other way of creating this linked service is to specify resource group name and data factory name instead of specifying the DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="fd2fe-206">Creación de un servicio vinculado para una instancia de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="fd2fe-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="fd2fe-207">En este paso, vinculará su cuenta de Base de datos SQL de Azure con su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-207">In this step, you link your Azure SQL database to your data factory.</span></span>

1. <span data-ttu-id="fd2fe-208">Cree un archivo JSON con el nombre AzureSqlLinkedService.json en la carpeta C:\ADFGetStartedPSH con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fd2fe-209">Reemplace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; y &lt;password&gt; por los nombres del servidor SQL Azure, de la base de datos, de la cuenta de usuario y de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="fd2fe-210">Ejecute el siguiente comando para crear un servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-210">Run the following command to create a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="fd2fe-211">Este es la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-211">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="fd2fe-212">Confirme que la opción **Permitir el acceso a los servicios de Azure** esté activada para el servidor de bases de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-212">Confirm that **Allow access to Azure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="fd2fe-213">Para comprobarla y activarla, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-213">To verify and turn it on, do the following steps:</span></span>

    1. <span data-ttu-id="fd2fe-214">Inicie sesión en el [Azure Portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="fd2fe-214">Log in to the [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="fd2fe-215">Haga clic en **Más servicios >** a la izquierda, y haga clic en **Servidores SQL** en la categoría **BASES DE DATOS**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-215">Click **More services >** on the left, and click **SQL servers** in the **DATABASES** category.</span></span>
    3. <span data-ttu-id="fd2fe-216">Seleccione el servidor en la lista de servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-216">Select your server in the list of SQL servers.</span></span>
    4. <span data-ttu-id="fd2fe-217">En la hoja SQL Server, haga clic en el vínculo **Mostrar configuración del firewall**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-217">On the SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="fd2fe-218">En la hoja **Configuración de firewall**, haga clic en **ACTIVADA** para **Permitir el acceso a los servicios de Azure**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-218">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
    6. <span data-ttu-id="fd2fe-219">Haga clic en **Guardar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-219">Click **Save** on the toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="fd2fe-220">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="fd2fe-220">Create datasets</span></span>
<span data-ttu-id="fd2fe-221">En el paso anterior, creó servicios vinculados para vincular una cuenta de Azure Storage y una base de datos SQL de Azure con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-221">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="fd2fe-222">En este paso, defina dos conjuntos de datos llamados InputDataset y OutputDataset, que representan los datos de entrada y salida que se almacenan en los almacenes de datos a los que hacen referencia AzureStorageLinkedService y AzureSqlLinkedService, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="fd2fe-223">El servicio vinculado Azure Storage especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-223">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="fd2fe-224">Además, el conjunto de datos de blobs de entrada (InputDataset) especifica el contenedor y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-224">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="fd2fe-225">De forma similar, el servicio vinculado Azure SQL Database especifica la cadena de conexión que el servicio Data Factory utiliza en tiempo de ejecución para conectarse a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-225">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="fd2fe-226">Además, el conjunto de datos de la tabla SQL de salida (OutputDataset) especifica la tabla de la base de datos en la que se copian los datos de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-226">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="fd2fe-227">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="fd2fe-227">Create an input dataset</span></span>
<span data-ttu-id="fd2fe-228">En este paso, se crea un conjunto de datos llamado InputDataset, que apunta a un archivo de blobs (emp.txt) en la carpeta raíz de un contenedor de blobs (adftutorial), en la instancia de Azure Storage representada por el servicio vinculado AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-228">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="fd2fe-229">Si no especifica un valor para fileName (o puede omitirlo), los datos de todos los blobs en la carpeta de entrada se copian en el destino.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-229">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="fd2fe-230">En este tutorial, especifique un valor para fileName.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-230">In this tutorial, you specify a value for the fileName.</span></span>  

1. <span data-ttu-id="fd2fe-231">Cree un archivo JSON llamado **InputDataset.json** en la carpeta **C:\ADFGetStartedPSH** con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-231">Create a JSON file named **InputDataset.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

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
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
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

    <span data-ttu-id="fd2fe-232">En la siguiente tabla se ofrecen descripciones de las propiedades JSON que se usan en el fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-232">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="fd2fe-233">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fd2fe-233">Property</span></span> | <span data-ttu-id="fd2fe-234">Descripción</span><span class="sxs-lookup"><span data-stu-id="fd2fe-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="fd2fe-235">type</span><span class="sxs-lookup"><span data-stu-id="fd2fe-235">type</span></span> | <span data-ttu-id="fd2fe-236">La propiedad type se establece en **AzureBlob** porque los datos residen en una instancia de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-236">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="fd2fe-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fd2fe-237">linkedServiceName</span></span> | <span data-ttu-id="fd2fe-238">Hace referencia al servicio **AzureStorageLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-238">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="fd2fe-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="fd2fe-239">folderPath</span></span> | <span data-ttu-id="fd2fe-240">Especifica el **contenedor** de blobs y la **carpeta** que contiene los blobs de entrada.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-240">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="fd2fe-241">En este tutorial, adftutorial es el contenedor de blobs y folder es la carpeta raíz.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-241">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="fd2fe-242">fileName</span><span class="sxs-lookup"><span data-stu-id="fd2fe-242">fileName</span></span> | <span data-ttu-id="fd2fe-243">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-243">This property is optional.</span></span> <span data-ttu-id="fd2fe-244">Si omite esta propiedad, se seleccionan todos los archivos de folderPath.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-244">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="fd2fe-245">En este tutorial, se especifica **emp.txt** en fileName, por lo que solo se selecciona ese archivo para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-245">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="fd2fe-246">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="fd2fe-246">format -> type</span></span> |<span data-ttu-id="fd2fe-247">El archivo de entrada tiene formato de texto, por lo que usamos **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-247">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="fd2fe-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="fd2fe-248">columnDelimiter</span></span> | <span data-ttu-id="fd2fe-249">Las columnas del archivo de entrada están delimitadas por **coma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-249">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="fd2fe-250">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="fd2fe-250">frequency/interval</span></span> | <span data-ttu-id="fd2fe-251">La frecuencia está establecida en **Hour** y el intervalo es **1**, lo que significa que los segmentos de entrada estarán disponibles **cada hora**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-251">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="fd2fe-252">En otras palabras, el servicio Data Factory busca los datos de entrada cada hora en la carpeta raíz del contenedor de blobs (**adftutorial**) que se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-252">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="fd2fe-253">Busca los datos entre las horas de inicio y finalización de la canalización, no antes ni después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-253">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="fd2fe-254">external</span><span class="sxs-lookup"><span data-stu-id="fd2fe-254">external</span></span> | <span data-ttu-id="fd2fe-255">Esta propiedad se establece en **true** si esta canalización no ha generado los datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-255">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="fd2fe-256">Los datos de entrada de este tutorial están en el archivo emp.txt, que no lo generó esta canalización, por lo que establecemos esta propiedad en true.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-256">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="fd2fe-257">Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="fd2fe-258">Ejecute el comando siguiente para crear el conjunto de datos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-258">Run the following command to create the Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="fd2fe-259">Este es la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-259">Here is the sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="fd2fe-260">Crear un conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="fd2fe-260">Create an output dataset</span></span>
<span data-ttu-id="fd2fe-261">En esta parte del paso se crea un conjunto de datos de salida denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-261">In this part of the step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="fd2fe-262">Este conjunto de datos apunta a una tabla SQL de Azure SQL Database representada por **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-262">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="fd2fe-263">Cree un archivo JSON llamado **OutputDataset.json** en la carpeta **C:\ADFGetStartedPSH** con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-263">Create a JSON file named **OutputDataset.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span></span>

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
            "linkedServiceName": "AzureSqlLinkedService",
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

    <span data-ttu-id="fd2fe-264">En la siguiente tabla se ofrecen descripciones de las propiedades JSON que se usan en el fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-264">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="fd2fe-265">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fd2fe-265">Property</span></span> | <span data-ttu-id="fd2fe-266">Descripción</span><span class="sxs-lookup"><span data-stu-id="fd2fe-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="fd2fe-267">type</span><span class="sxs-lookup"><span data-stu-id="fd2fe-267">type</span></span> | <span data-ttu-id="fd2fe-268">La propiedad type se establece en **AzureSqlTable** porque los datos se copian en una tabla de una base de datos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-268">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="fd2fe-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fd2fe-269">linkedServiceName</span></span> | <span data-ttu-id="fd2fe-270">Hace referencia al servicio **AzureSqlLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-270">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="fd2fe-271">tableName</span><span class="sxs-lookup"><span data-stu-id="fd2fe-271">tableName</span></span> | <span data-ttu-id="fd2fe-272">Especifica la **tabla** en la que se copian los datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-272">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="fd2fe-273">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="fd2fe-273">frequency/interval</span></span> | <span data-ttu-id="fd2fe-274">La frecuencia se establece en **Hour** y el intervalo es **1**, lo que significa que los sectores de salida se producen **cada hora** entre las horas de inicio y finalización de la canalización, no antes ni después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-274">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="fd2fe-275">En la tabla emp de la base de datos hay tres columnas: **ID**, **FirstName** y **LastName**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-275">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="fd2fe-276">ID es una columna de identidad, por lo que deberá especificar solo **FirstName** y **LastName** aquí.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-276">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="fd2fe-277">Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="fd2fe-278">Ejecute el comando siguiente para crear el conjunto de datos de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-278">Run the following command to create the data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="fd2fe-279">Este es la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-279">Here is the sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="fd2fe-280">Crear una canalización</span><span class="sxs-lookup"><span data-stu-id="fd2fe-280">Create a pipeline</span></span>
<span data-ttu-id="fd2fe-281">En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="fd2fe-282">Actualmente, el conjunto de datos de salida es lo que impulsa la programación.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-282">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="fd2fe-283">En este tutorial, el conjunto de datos de salida está configurado para generar un segmento una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-283">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="fd2fe-284">La canalización tiene una hora de inicio y una hora de finalización con un día de diferencia, es decir, 24 horas.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-284">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="fd2fe-285">Por lo tanto, la canalización produce 24 segmentos del conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-285">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 


1. <span data-ttu-id="fd2fe-286">Cree un archivo JSON llamado **ADFTutorialPipeline.json** en la carpeta **C:\ADFGetStartedPSH** con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-286">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    <span data-ttu-id="fd2fe-287">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-287">Note the following points:</span></span>
   
    - <span data-ttu-id="fd2fe-288">En la sección de actividades, solo hay una actividad con **type** establecido en **Copy**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="fd2fe-289">Para más información acerca de la actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-289">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="fd2fe-290">En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="fd2fe-291">La entrada de la actividad está establecida en **InputDataset**, mientras que la salida está establecida en **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="fd2fe-292">En la sección **typeProperties**, **BlobSource** se especifica como el tipo de origen y **SqlSink** como el tipo de receptor.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="fd2fe-293">Consulte la lista de [almacenes de datos que se admiten](data-factory-data-movement-activities.md#supported-data-stores-and-formats) como orígenes y receptores de la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-293">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fd2fe-294">Para más información sobre cómo usar un almacén de datos admitido específico como receptor de origen, haga clic en el vínculo en la tabla.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-294">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="fd2fe-295">Reemplace el valor de la propiedad **start** por el día actual y el valor **end** por el próximo día.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-295">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="fd2fe-296">Puede especificar solo la parte de fecha y omitir la parte de hora de la fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-296">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="fd2fe-297">Por ejemplo, "03-02-2016", que es equivalente a "03-02-2016T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="fd2fe-297">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="fd2fe-298">Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="fd2fe-299">Por ejemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="fd2fe-300">La hora de finalización ( **end** ) es opcional, pero se utilizará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-300">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="fd2fe-301">Si no especifica ningún valor para la propiedad **end**, se calcula como "**start + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="fd2fe-301">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="fd2fe-302">Para ejecutar la canalización indefinidamente, especifique **9999-09-09** como valor de propiedad **end**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-302">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="fd2fe-303">En el ejemplo anterior hay 24 segmentos de datos, ya que cada segmento de datos se produce cada hora.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-303">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="fd2fe-304">Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fd2fe-305">Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="fd2fe-306">Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="fd2fe-307">Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="fd2fe-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="fd2fe-308">Ejecute el comando siguiente para crear la tabla de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-308">Run the following command to create the data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="fd2fe-309">Este es la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-309">Here is the sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="fd2fe-310">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="fd2fe-310">**Congratulations!**</span></span> <span data-ttu-id="fd2fe-311">Ha creado correctamente una factoría de datos de Azure, con una canalización para copiar datos desde Azure Blob Storage a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-311">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

## <a name="monitor-the-pipeline"></a><span data-ttu-id="fd2fe-312">Supervisar la canalización</span><span class="sxs-lookup"><span data-stu-id="fd2fe-312">Monitor the pipeline</span></span>
<span data-ttu-id="fd2fe-313">En este paso, se usa Azure PowerShell para supervisar lo que ocurre en una Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-313">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="fd2fe-314">Reemplace &lt;DataFactoryName&gt; por el nombre de la factoría de datos, ejecute **Get-AzureRmDataFactory**, y asigne el resultado a una variable $df.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-314">Replace &lt;DataFactoryName&gt; with the name of your data factory and run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="fd2fe-315">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="fd2fe-316">Después, imprima el contenido de $df para ver el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-316">Then, run print the contents of $df to see the following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="fd2fe-317">Ejecute **Get-AzureRmDataFactorySlice** para obtener la información sobre todos los segmentos de **OutputDataset**, que es el conjunto de datos de salida de la canalización.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-317">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **OutputDataset**, which is the output dataset of the pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="fd2fe-318">Esta configuración debe coincidir con el valor de **Inicio** del JSON de canalización.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-318">This setting should match the **Start** value in the pipeline JSON.</span></span> <span data-ttu-id="fd2fe-319">Debe ver 24 segmentos, uno para cada hora de 12 A.M. del día actual hasta las 12 A.M. del día siguiente.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-319">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span></span>

   <span data-ttu-id="fd2fe-320">Estos son tres segmentos de ejemplo de la salida:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-320">Here are three sample slices from the output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="fd2fe-321">Ejecute **Get-AzureRmDataFactoryRun** para obtener la información de la actividad que se ejecuta para un segmento **específico**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-321">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="fd2fe-322">Copie el valor de fecha y hora de la salida del comando anterior para especificar el valor del parámetro StartDateTime.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-322">Copy the date-time value from the output of the previous command to specify the value for the StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="fd2fe-323">Este es la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-323">Here is the sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="fd2fe-324">Consulte [Referencia de cmdlets de Data Factory](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre los cmdlets de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="fd2fe-325">Resumen</span><span class="sxs-lookup"><span data-stu-id="fd2fe-325">Summary</span></span>
<span data-ttu-id="fd2fe-326">En este tutorial, ha creado una factoría de datos de Azure para copiar datos de un blob de Azure en una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-326">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="fd2fe-327">Ha usado PowerShell para crear la factoría de datos, los servicios vinculados, los conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-327">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="fd2fe-328">Estos son los pasos de alto nivel que realizó en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-328">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="fd2fe-329">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="fd2fe-330">Ha creado **servicios vinculados**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-330">Created **linked services**:</span></span>

   <span data-ttu-id="fd2fe-331">a.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-331">a.</span></span> <span data-ttu-id="fd2fe-332">Un servicio vinculado **Azure Storage** para vincular la cuenta de almacenamiento de Azure que contiene datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-332">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="fd2fe-333">b.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-333">b.</span></span> <span data-ttu-id="fd2fe-334">Un servicio vinculado **Azure SQL** para vincular la base de datos SQL que contiene los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-334">An **Azure SQL** linked service to link your SQL database that holds the output data.</span></span>
3. <span data-ttu-id="fd2fe-335">Ha creado **conjuntos de datos** que describen los datos de entrada y salida de las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="fd2fe-336">Ha creado una **canalización** con una **actividad de copia** con un origen **BlobSource** y un receptor **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd2fe-337">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd2fe-337">Next steps</span></span>
<span data-ttu-id="fd2fe-338">En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="fd2fe-339">En la tabla siguiente se proporciona una lista de almacenes de datos que se admiten como orígenes y destinos de la actividad de copia:</span><span class="sxs-lookup"><span data-stu-id="fd2fe-339">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="fd2fe-340">Para aprender a copiar datos hacia y desde un almacén de datos, haga clic en el vínculo del almacén de datos en la tabla.</span><span class="sxs-lookup"><span data-stu-id="fd2fe-340">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span> 

