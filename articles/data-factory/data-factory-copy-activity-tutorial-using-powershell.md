---
title: "Tutorial: Crear una canalización de datos de toomove mediante el uso de PowerShell de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="c22f2-103">Tutorial: Creación de una canalización de Data Factory para mover datos mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c22f2-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c22f2-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c22f2-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="c22f2-105">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="c22f2-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="c22f2-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c22f2-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="c22f2-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c22f2-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="c22f2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c22f2-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="c22f2-109">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c22f2-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="c22f2-110">API DE REST</span><span class="sxs-lookup"><span data-stu-id="c22f2-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="c22f2-111">API de .NET</span><span class="sxs-lookup"><span data-stu-id="c22f2-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="c22f2-112">En este artículo, aprenderá cómo toouse PowerShell toocreate una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="c22f2-113">Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c22f2-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="c22f2-114">En este tutorial, creará una canalización con una actividad en ella: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="c22f2-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="c22f2-115">actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos.</span><span class="sxs-lookup"><span data-stu-id="c22f2-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="c22f2-116">Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c22f2-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c22f2-117">actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="c22f2-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="c22f2-118">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="c22f2-119">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="c22f2-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c22f2-120">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="c22f2-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c22f2-121">Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c22f2-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="c22f2-122">Este artículo no cubre todos los cmdlets de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="c22f2-123">Vea [Referencia de cmdlets de Data Factory](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre estos cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c22f2-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="c22f2-124">canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="c22f2-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="c22f2-125">Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c22f2-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c22f2-126">Prerequisites</span></span>
- <span data-ttu-id="c22f2-127">Complete los requisitos previos descritos en hello [requisitos previos tutoriales](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="c22f2-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="c22f2-128">Instale **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="c22f2-129">Siga las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="c22f2-130">Pasos</span><span class="sxs-lookup"><span data-stu-id="c22f2-130">Steps</span></span>
<span data-ttu-id="c22f2-131">Estos son los pasos de hello que realizar como parte de este tutorial:</span><span class="sxs-lookup"><span data-stu-id="c22f2-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="c22f2-132">Cree una **factoría de datos** de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="c22f2-133">En este paso, creará una factoría de datos llamada ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="c22f2-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="c22f2-134">Crear **servicios vinculados** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="c22f2-135">En este paso, se crean dos servicios vinculados del tipo Azure Storage y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c22f2-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="c22f2-136">Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c22f2-137">Crea un contenedor y cargar la cuenta de almacenamiento de datos toothis como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="c22f2-138">AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c22f2-139">datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="c22f2-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c22f2-140">Como parte de los [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), se creó una tabla SQL en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="c22f2-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="c22f2-141">Crear la entrada y salida **conjuntos de datos** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="c22f2-142">servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c22f2-143">Y el conjunto de datos de hello blob de entrada especifica el contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="c22f2-144">De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c22f2-145">Y conjunto de datos de tabla SQL de Hola salida especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c22f2-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="c22f2-146">Crear un **canalización** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="c22f2-147">En este paso, se crea una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="c22f2-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="c22f2-148">actividad de copia de Hello copia datos de un blob en la tabla de tooa de almacenamiento de blobs de Azure de hello en la base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="c22f2-149">Puede usar una actividad de copia en datos toocopy canalización desde cualquier origen compatibles tooany admitida el destino.</span><span class="sxs-lookup"><span data-stu-id="c22f2-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="c22f2-150">Para ver una lista de los almacenes de datos admitidos, consulte el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c22f2-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="c22f2-151">Canalización de Hola de monitor.</span><span class="sxs-lookup"><span data-stu-id="c22f2-151">Monitor hello pipeline.</span></span> <span data-ttu-id="c22f2-152">En este paso, se **monitor** Hola sectores de conjuntos de datos de entrada y salida mediante el uso de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c22f2-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="c22f2-153">Crear una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="c22f2-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c22f2-154">Completa [requisitos previos para el tutorial de hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="c22f2-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="c22f2-155">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="c22f2-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c22f2-156">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="c22f2-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c22f2-157">Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de salida de tooproduct de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c22f2-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="c22f2-158">Puede empezar con la creación de factoría de datos de hello en este paso.</span><span class="sxs-lookup"><span data-stu-id="c22f2-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="c22f2-159">Inicie **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-159">Launch **PowerShell**.</span></span> <span data-ttu-id="c22f2-160">Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c22f2-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="c22f2-161">Si cerrar y volver a abrir, se necesitan toorun comandos de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c22f2-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="c22f2-162">Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="c22f2-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="c22f2-163">Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta:</span><span class="sxs-lookup"><span data-stu-id="c22f2-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="c22f2-164">Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.</span><span class="sxs-lookup"><span data-stu-id="c22f2-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="c22f2-165">Reemplace  **&lt;NameOfAzureSubscription** &gt; con el nombre de Hola de su suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="c22f2-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="c22f2-166">Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c22f2-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="c22f2-167">Algunos de los pasos de hello en este tutorial se supone que usa grupo de recursos de hello llamado **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="c22f2-168">Si utiliza un grupo de recursos diferente, deberá toouse, en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c22f2-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="c22f2-169">Ejecute hello **New-AzureRmDataFactory** una factoría de datos con el nombre del cmdlet toocreate **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="c22f2-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="c22f2-170">Puede que ya se esté usando este nombre.</span><span class="sxs-lookup"><span data-stu-id="c22f2-170">This name may already have been taken.</span></span> <span data-ttu-id="c22f2-171">Por lo tanto, asegúrese de nombre Hola Hola factoría de datos único mediante la adición de un prefijo o sufijo (por ejemplo: ADFTutorialDataFactoryPSH05152017) y vuelva a ejecutar el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="c22f2-172">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="c22f2-172">Note hello following points:</span></span>

* <span data-ttu-id="c22f2-173">nombre de Hola Hola Azure factoría de datos debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="c22f2-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="c22f2-174">Si recibes Hola tras error, cambie el nombre de hello (por ejemplo, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="c22f2-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="c22f2-175">Use este nombre en lugar de ADFTutorialFactoryPSH mientras lleva a cabo los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c22f2-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="c22f2-176">Consulte [Data Factory: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c22f2-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="c22f2-177">instancias de la factoría de datos de toocreate, debe ser un colaborador o administrador de hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="c22f2-178">nombre Hola Hola factoría de datos puede registrado como un nombre DNS en hello futuras y por lo tanto, están visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="c22f2-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="c22f2-179">Es posible que reciba Hola siguiente error: "**esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory.**"</span><span class="sxs-lookup"><span data-stu-id="c22f2-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="c22f2-180">Siga uno de los procedimientos de Hola e intente publicar de nuevo:</span><span class="sxs-lookup"><span data-stu-id="c22f2-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="c22f2-181">En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="c22f2-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="c22f2-182">Ejecute hello después comando tooconfirm ese Hola factoría de datos de proveedor está registrado:</span><span class="sxs-lookup"><span data-stu-id="c22f2-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="c22f2-183">Inicio de sesión mediante el uso de Hola toohello de suscripción de Azure [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c22f2-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c22f2-184">Visite tooa hoja de factoría de datos o crear una factoría de datos en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="c22f2-185">Esta acción registra automáticamente proveedor Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="c22f2-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c22f2-186">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="c22f2-186">Create linked services</span></span>
<span data-ttu-id="c22f2-187">Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="c22f2-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="c22f2-188">En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c22f2-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="c22f2-189">Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino).</span><span class="sxs-lookup"><span data-stu-id="c22f2-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="c22f2-190">Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="c22f2-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="c22f2-191">Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c22f2-192">Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="c22f2-193">AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c22f2-194">datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="c22f2-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c22f2-195">Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="c22f2-196">Creación de un servicio vinculado para una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c22f2-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="c22f2-197">En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="c22f2-198">Cree un archivo JSON denominado **AzureStorageLinkedService.json** en **C:\ADFGetStartedPSH** carpeta con hello siguen contenido: (crear Hola carpeta ADFGetStartedPSH si aún no existe.)</span><span class="sxs-lookup"><span data-stu-id="c22f2-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c22f2-199">Reemplace &lt;accountname&gt; y &lt;accountkey&gt; con nombre y clave de la cuenta de almacenamiento de Azure antes de guardar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="c22f2-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

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
2. <span data-ttu-id="c22f2-200">En **Azure PowerShell**, cambiar toohello **ADFGetStartedPSH** carpeta.</span><span class="sxs-lookup"><span data-stu-id="c22f2-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="c22f2-201">Ejecute hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate Hola servicio vinculado: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="c22f2-202">Este cmdlet y otros cmdlets de factoría de datos que se usa en este tutorial requiere que los valores de toopass para hello **ResourceGroupName** y **DataFactoryName** parámetros.</span><span class="sxs-lookup"><span data-stu-id="c22f2-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="c22f2-203">Como alternativa, puede pasar Hola DataFactory devueltas mediante el cmdlet New-AzureRmDataFactory Hola sin escribir ResourceGroupName y DataFactoryName cada vez que se ejecuta un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c22f2-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="c22f2-204">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c22f2-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="c22f2-205">Otra manera de crear este servicio vinculado es toospecify nombre de grupo de recursos y el nombre de generador de datos en lugar de especificar el objeto de hello DataFactory.</span><span class="sxs-lookup"><span data-stu-id="c22f2-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="c22f2-206">Creación de un servicio vinculado para una instancia de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c22f2-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="c22f2-207">En este paso, vincule la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="c22f2-208">Cree un archivo JSON denominado AzureSqlLinkedService.json en la carpeta C:\ADFGetStartedPSH con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="c22f2-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c22f2-209">Reemplace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; y &lt;password&gt; por los nombres del servidor SQL Azure, de la base de datos, de la cuenta de usuario y de la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c22f2-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
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
2. <span data-ttu-id="c22f2-210">Ejecute hello después comando toocreate un servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="c22f2-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="c22f2-211">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c22f2-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="c22f2-212">Confirme que **permitir acceso a servicios de tooAzure** esté activada para el servidor de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c22f2-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="c22f2-213">tooverify y activarla, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c22f2-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="c22f2-214">Inicie sesión en toohello [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="c22f2-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="c22f2-215">Haga clic en **más servicios >** Hola izquierda y haga clic en **servidores SQL Server** en hello **bases de datos** categoría.</span><span class="sxs-lookup"><span data-stu-id="c22f2-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="c22f2-216">Seleccione el servidor en la lista de Hola de servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c22f2-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="c22f2-217">En la hoja de hello SQL server, haga clic en **mostrar configuraciones de firewall** vínculo.</span><span class="sxs-lookup"><span data-stu-id="c22f2-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="c22f2-218">Hola **configuración del Firewall** hoja, haga clic en **ON** para **permitir acceso a servicios de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="c22f2-219">Haga clic en **guardar** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="c22f2-220">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="c22f2-220">Create datasets</span></span>
<span data-ttu-id="c22f2-221">En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="c22f2-222">En este paso, definirá dos conjuntos de datos con el nombre InputDataset y OutputDataset que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService y AzureSqlLinkedService respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c22f2-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="c22f2-223">servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c22f2-224">Y conjunto de datos de blob de entrada de hello (InputDataset) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="c22f2-225">De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c22f2-226">Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c22f2-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="c22f2-227">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="c22f2-227">Create an input dataset</span></span>
<span data-ttu-id="c22f2-228">En este paso, creará un conjunto de datos denominado InputDataset que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService vinculado servicio de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="c22f2-229">Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="c22f2-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="c22f2-230">En este tutorial, especifique un valor para el nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="c22f2-231">Cree un archivo JSON denominado **InputDataset.json** en hello **C:\ADFGetStartedPSH** carpeta, con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="c22f2-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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

    <span data-ttu-id="c22f2-232">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="c22f2-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c22f2-233">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c22f2-233">Property</span></span> | <span data-ttu-id="c22f2-234">Descripción</span><span class="sxs-lookup"><span data-stu-id="c22f2-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c22f2-235">type</span><span class="sxs-lookup"><span data-stu-id="c22f2-235">type</span></span> | <span data-ttu-id="c22f2-236">propiedad de tipo Hello se establece demasiado**AzureBlob** porque los datos residen en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="c22f2-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c22f2-237">linkedServiceName</span></span> | <span data-ttu-id="c22f2-238">Hace referencia a toohello **AzureStorageLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c22f2-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c22f2-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="c22f2-239">folderPath</span></span> | <span data-ttu-id="c22f2-240">Especifica el blob de hello **contenedor** hello y **carpeta** que contiene la entrada de blobs.</span><span class="sxs-lookup"><span data-stu-id="c22f2-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="c22f2-241">En este tutorial, adftutorial es el contenedor de blob de Hola y carpeta es la carpeta raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="c22f2-242">fileName</span><span class="sxs-lookup"><span data-stu-id="c22f2-242">fileName</span></span> | <span data-ttu-id="c22f2-243">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="c22f2-243">This property is optional.</span></span> <span data-ttu-id="c22f2-244">Si se omite esta propiedad, se seleccionan todos los archivos de hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="c22f2-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="c22f2-245">En este tutorial, **emp.txt** se especificó para hello nombre de archivo, por lo que sólo ese archivo se recoge para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="c22f2-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="c22f2-246">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="c22f2-246">format -> type</span></span> |<span data-ttu-id="c22f2-247">archivo de entrada de Hello es hello en formato de texto, por lo que usamos **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="c22f2-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c22f2-248">columnDelimiter</span></span> | <span data-ttu-id="c22f2-249">columnas de Hello en el archivo de entrada de Hola se delimitan mediante **carácter de coma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="c22f2-250">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="c22f2-250">frequency/interval</span></span> | <span data-ttu-id="c22f2-251">frecuencia de Hola se establece demasiado**hora** e intervalo está establecido demasiado**1**, lo que significa que Hola entrada sectores están disponibles **cada hora**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="c22f2-252">En otras palabras, Hola servicio Data Factory busca datos de entrada cada hora en carpeta de raíz de hello del contenedor de blobs (**adftutorial**) que especificó.</span><span class="sxs-lookup"><span data-stu-id="c22f2-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="c22f2-253">Busca datos Hola Hola canalización inicio y finalización horas, no antes o después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="c22f2-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="c22f2-254">external</span><span class="sxs-lookup"><span data-stu-id="c22f2-254">external</span></span> | <span data-ttu-id="c22f2-255">Esta propiedad se establece demasiado**true** si no se generan datos de hello esta canalización.</span><span class="sxs-lookup"><span data-stu-id="c22f2-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="c22f2-256">datos de entrada de Hello en este tutorial están en el archivo emp.txt de hello, que no se genera esta canalización, por lo que se establece esta propiedad tootrue.</span><span class="sxs-lookup"><span data-stu-id="c22f2-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="c22f2-257">Para más información acerca de estas propiedades JSON, consulte el [artículo sobre el conector de blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c22f2-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="c22f2-258">Ejecute hello siguiendo el conjunto de datos de comando toocreate Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="c22f2-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="c22f2-259">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c22f2-259">Here is hello sample output:</span></span>

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

### <a name="create-an-output-dataset"></a><span data-ttu-id="c22f2-260">Crear un conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="c22f2-260">Create an output dataset</span></span>
<span data-ttu-id="c22f2-261">En esta parte del paso de hello, se crea un conjunto de datos de salida denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="c22f2-262">Este conjunto de datos señala tooa table de SQL de base de datos de SQL Azure de hello representado por **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="c22f2-263">Cree un archivo JSON denominado **OutputDataset.json** en hello **C:\ADFGetStartedPSH** carpeta con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="c22f2-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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

    <span data-ttu-id="c22f2-264">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="c22f2-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c22f2-265">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c22f2-265">Property</span></span> | <span data-ttu-id="c22f2-266">Descripción</span><span class="sxs-lookup"><span data-stu-id="c22f2-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c22f2-267">type</span><span class="sxs-lookup"><span data-stu-id="c22f2-267">type</span></span> | <span data-ttu-id="c22f2-268">propiedad de tipo Hello se establece demasiado**AzureSqlTable** porque datos están la tabla de tooa copiado en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="c22f2-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c22f2-269">linkedServiceName</span></span> | <span data-ttu-id="c22f2-270">Hace referencia a toohello **AzureSqlLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c22f2-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c22f2-271">tableName</span><span class="sxs-lookup"><span data-stu-id="c22f2-271">tableName</span></span> | <span data-ttu-id="c22f2-272">Hola especificado **tabla** toowhich Hola datos se copian.</span><span class="sxs-lookup"><span data-stu-id="c22f2-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="c22f2-273">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="c22f2-273">frequency/interval</span></span> | <span data-ttu-id="c22f2-274">Hello frecuencia se establece demasiado**hora** y el intervalo es **1**, lo que significa que se producen los sectores de salida de hello **cada hora** entre el inicio de la canalización de Hola y de finalización veces, no antes o Después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="c22f2-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="c22f2-275">Hay tres columnas: **identificador**, **FirstName**, y **LastName** : en la tabla emp de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="c22f2-276">Id. es una columna de identidad, por lo que necesita solo toospecify **FirstName** y **LastName** aquí.</span><span class="sxs-lookup"><span data-stu-id="c22f2-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="c22f2-277">Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c22f2-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="c22f2-278">Ejecute hello siguiendo el conjunto de datos de la factoría de datos de comando toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="c22f2-279">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c22f2-279">Here is hello sample output:</span></span>

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

## <a name="create-a-pipeline"></a><span data-ttu-id="c22f2-280">Crear una canalización</span><span class="sxs-lookup"><span data-stu-id="c22f2-280">Create a pipeline</span></span>
<span data-ttu-id="c22f2-281">En este paso, creará una canalización con una **actividad de copia** que utiliza **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="c22f2-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="c22f2-282">Actualmente, el conjunto de datos de salida es qué unidades Hola programación.</span><span class="sxs-lookup"><span data-stu-id="c22f2-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="c22f2-283">En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="c22f2-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="c22f2-284">canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="c22f2-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="c22f2-285">Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="c22f2-286">Cree un archivo JSON denominado **ADFTutorialPipeline.json** en hello **C:\ADFGetStartedPSH** carpeta, con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="c22f2-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
    <span data-ttu-id="c22f2-287">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="c22f2-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="c22f2-288">En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="c22f2-289">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c22f2-290">En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="c22f2-291">Entrada de actividad hello se establece demasiado**InputDataset** y salida de actividad hello se establece demasiado**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="c22f2-292">Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="c22f2-293">Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c22f2-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c22f2-294">toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="c22f2-295">Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente.</span><span class="sxs-lookup"><span data-stu-id="c22f2-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="c22f2-296">Puede especificar sólo parte de fecha de Hola y omitir la parte de hora de Hola de hello fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="c22f2-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="c22f2-297">Por ejemplo, "2016-02-03", que es equivalente demasiado "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="c22f2-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="c22f2-298">Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c22f2-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c22f2-299">Por ejemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c22f2-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="c22f2-300">Hola **final** tiempo es opcional, pero se usa en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c22f2-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="c22f2-301">Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="c22f2-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="c22f2-302">canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.</span><span class="sxs-lookup"><span data-stu-id="c22f2-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="c22f2-303">En el anterior ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.</span><span class="sxs-lookup"><span data-stu-id="c22f2-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="c22f2-304">Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c22f2-305">Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c22f2-306">Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="c22f2-307">Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c22f2-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="c22f2-308">Ejecute hello después de la tabla de factoría de datos de comando toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="c22f2-309">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c22f2-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="c22f2-310">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="c22f2-310">**Congratulations!**</span></span> <span data-ttu-id="c22f2-311">Ha creado correctamente una factoría de datos de Azure con datos toocopy canalización desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="c22f2-312">Canalización de Hola de Monitor</span><span class="sxs-lookup"><span data-stu-id="c22f2-312">Monitor hello pipeline</span></span>
<span data-ttu-id="c22f2-313">En este paso, utilice toomonitor de PowerShell de Azure que está sucediendo en una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="c22f2-314">Reemplace &lt;DataFactoryName&gt; con el nombre de saludo de la factoría de datos y ejecute **AzureRmDataFactory Get**y asignar Hola salida tooa $df variable.</span><span class="sxs-lookup"><span data-stu-id="c22f2-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="c22f2-315">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c22f2-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="c22f2-316">A continuación, ejecute impresión Hola contenido $df toosee Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="c22f2-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
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
2. <span data-ttu-id="c22f2-317">Ejecutar **Get AzureRmDataFactorySlice** tooget obtener más información acerca de todos los sectores de hello **OutputDataset**, que es el conjunto de datos de salida de hello de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="c22f2-318">Esta configuración debe coincidir con hello **iniciar** valor en JSON de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="c22f2-319">Debería ver 24 sectores, uno para cada hora de 12 AM de Hola día actual too12 ESTOY de hello día siguiente.</span><span class="sxs-lookup"><span data-stu-id="c22f2-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="c22f2-320">A continuación, presentamos tres intervalos de ejemplo de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="c22f2-320">Here are three sample slices from hello output:</span></span> 

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
3. <span data-ttu-id="c22f2-321">Ejecutar **Get AzureRmDataFactoryRun** tooget Hola detalles de actividad se ejecuta durante un **específico** segmento.</span><span class="sxs-lookup"><span data-stu-id="c22f2-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="c22f2-322">Copiar valor de fecha y hora de Hola de salida de hello de hello comando toospecify Hola valor anterior para el parámetro de StartDateTime Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="c22f2-323">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c22f2-323">Here is hello sample output:</span></span> 

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

<span data-ttu-id="c22f2-324">Consulte [Referencia de cmdlets de Data Factory](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre los cmdlets de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c22f2-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="c22f2-325">Resumen</span><span class="sxs-lookup"><span data-stu-id="c22f2-325">Summary</span></span>
<span data-ttu-id="c22f2-326">En este tutorial, ha creado un datos toocopy de factoría de datos de Azure desde una base de datos de SQL Azure de tooan de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="c22f2-327">Ha utilizado la factoría de datos de PowerShell toocreate hello, servicios vinculados, conjuntos de datos y una canalización.</span><span class="sxs-lookup"><span data-stu-id="c22f2-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="c22f2-328">Estos son los pasos de alto nivel de hello realizadas en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="c22f2-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="c22f2-329">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="c22f2-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c22f2-330">Ha creado **servicios vinculados**.</span><span class="sxs-lookup"><span data-stu-id="c22f2-330">Created **linked services**:</span></span>

   <span data-ttu-id="c22f2-331">a.</span><span class="sxs-lookup"><span data-stu-id="c22f2-331">a.</span></span> <span data-ttu-id="c22f2-332">Un **el almacenamiento de Azure** vinculado toolink de servicio de su cuenta de almacenamiento de Azure que contiene datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="c22f2-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="c22f2-333">b.</span><span class="sxs-lookup"><span data-stu-id="c22f2-333">b.</span></span> <span data-ttu-id="c22f2-334">Un **SQL Azure** vinculado toolink de servicio en la base de datos SQL que contiene los datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c22f2-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="c22f2-335">Ha creado **conjuntos de datos** que describen los datos de entrada y salida de las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="c22f2-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="c22f2-336">Crea un **canalización** con **actividad de copia**, con **BlobSource** como origen de Hola y **SqlSink** como receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c22f2-337">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c22f2-337">Next steps</span></span>
<span data-ttu-id="c22f2-338">En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="c22f2-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="c22f2-339">Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello:</span><span class="sxs-lookup"><span data-stu-id="c22f2-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="c22f2-340">toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c22f2-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

