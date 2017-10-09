---
title: "aaaBuild su primera factoría de datos (PowerShell) | Documentos de Microsoft"
description: "En este tutorial, creará un de ejemplo de canalización de Data Factory de Azure mediante Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="18811-103">Tutorial: Compilación de la primera instancia de Azure Data Factory con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="18811-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="18811-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18811-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="18811-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="18811-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="18811-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="18811-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="18811-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18811-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="18811-108">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="18811-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="18811-109">API DE REST</span><span class="sxs-lookup"><span data-stu-id="18811-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="18811-110">En este artículo, use PowerShell de Azure toocreate su primera factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="18811-111">tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="18811-112">canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="18811-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="18811-113">Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce.</span><span class="sxs-lookup"><span data-stu-id="18811-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="18811-114">canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="18811-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="18811-115">canalización de datos de Hello en este tutorial transforma los datos de salida de tooproduce de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="18811-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="18811-116">No copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="18811-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="18811-117">Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="18811-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="18811-118">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="18811-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="18811-119">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="18811-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="18811-120">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="18811-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18811-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="18811-121">Prerequisites</span></span>
* <span data-ttu-id="18811-122">Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="18811-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="18811-123">Siga las instrucciones de [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo tooinstall versión más reciente de PowerShell de Azure en el equipo.</span><span class="sxs-lookup"><span data-stu-id="18811-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="18811-124">(opcional) Este artículo no cubre todos los cmdlets de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="18811-125">Vea [Referencia de cmdlets de factoría de datos](/powershell/module/azurerm.datafactories) para obtener la documentación completa sobre los cmdlets de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="18811-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="18811-126">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="18811-126">Create data factory</span></span>
<span data-ttu-id="18811-127">En este paso, usar Azure PowerShell toocreate una factoría de datos de Azure denominado **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="18811-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="18811-128">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="18811-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="18811-129">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="18811-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="18811-130">Por ejemplo, una toocopy de datos de actividad de copia de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight un tootransform de script de Hive datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="18811-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="18811-131">Puede empezar con la creación de factoría de datos de hello en este paso.</span><span class="sxs-lookup"><span data-stu-id="18811-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="18811-132">Inicie PowerShell de Azure y ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="18811-133">Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18811-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="18811-134">Si se cierre y vuelva a abrir, deberá toorun estos comandos nuevo.</span><span class="sxs-lookup"><span data-stu-id="18811-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="18811-135">Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="18811-136">Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="18811-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="18811-137">Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.</span><span class="sxs-lookup"><span data-stu-id="18811-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="18811-138">Esta suscripción debe ser Hola igual que la que usó en el portal de Azure Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="18811-139">Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="18811-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="18811-140">Algunos de los pasos de hello en este tutorial se supone que usa el grupo de recursos de hello llamado ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="18811-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="18811-141">Si utiliza un grupo de recursos diferente, deberá toouse, en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18811-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="18811-142">Ejecute hello **New-AzureRmDataFactory** cmdlet que crea un generador de datos denominado **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="18811-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="18811-143">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="18811-143">Note hello following points:</span></span>

* <span data-ttu-id="18811-144">nombre de Hola de hello Data Factory de Azure debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="18811-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="18811-145">Si recibe el error hello **nombre de generador de datos "FirstDataFactoryPSH" no está disponible**, cambie el nombre de hello (por ejemplo, yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="18811-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="18811-146">Use este nombre en lugar de ADFTutorialFactoryPSH mientras lleva a cabo los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18811-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="18811-147">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="18811-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="18811-148">instancias de la factoría de datos de toocreate, deberá toobe un colaborador o administrador de hello suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="18811-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="18811-149">nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, se convierten en visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="18811-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="18811-150">Si recibe el error hello: "**esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory**", siga uno de los procedimientos de Hola e intente publicar de nuevo:</span><span class="sxs-lookup"><span data-stu-id="18811-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="18811-151">En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="18811-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="18811-152">Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado:</span><span class="sxs-lookup"><span data-stu-id="18811-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="18811-153">Inicio de sesión mediante Hola suscripción de Azure en hello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="18811-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="18811-154">Esta acción registra automáticamente proveedor Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="18811-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="18811-155">Antes de crear una canalización, necesita toocreate algunas entidades de la factoría de datos en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="18811-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="18811-156">En primer lugar crear servicios vinculados toolink datos almacenes/calcula tooyour almacenarán, definen la entrada y salida de datos de entrada/salida de toorepresent de conjuntos de datos en almacenes de datos vinculado como los datos, a continuación, crear canalización Hola con una actividad que usa estos conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="18811-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="18811-157">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="18811-157">Create linked services</span></span>
<span data-ttu-id="18811-158">En este paso, vincular su cuenta de almacenamiento de Azure y un generador de datos a petición tooyour de clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="18811-159">Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="18811-160">Hola servicio vinculado de HDInsight es toorun usa un script de Hive especificado en la actividad de hello de canalización de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="18811-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="18811-161">Identificar qué datos del almacén o proceso servicios se usan en el escenario y vinculan esos factoría de datos de servicios toohello mediante la creación de servicios vinculados.</span><span class="sxs-lookup"><span data-stu-id="18811-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="18811-162">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="18811-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="18811-163">En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="18811-164">Usar hello misma cuenta de almacenamiento de Azure hello HQL y datos de entrada/salida de toostore los archivos de scripts.</span><span class="sxs-lookup"><span data-stu-id="18811-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="18811-165">Cree un archivo JSON con el nombre StorageLinkedService.json en la carpeta de hello C:\ADFGetStarted con hello después de contenido.</span><span class="sxs-lookup"><span data-stu-id="18811-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="18811-166">Crear carpeta de hello ADFGetStarted si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="18811-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="18811-167">Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de almacenamiento de Azure y **clave de cuenta** por clave de acceso de Hola de hello cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="18811-168">toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="18811-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="18811-169">En Azure PowerShell, cambie toohello ADFGetStarted carpeta.</span><span class="sxs-lookup"><span data-stu-id="18811-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="18811-170">Puede usar hello **AzureRmDataFactoryLinkedService New** cmdlet que crea un servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="18811-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="18811-171">Este cmdlet y otros cmdlets de factoría de datos que se usa en este tutorial requiere que los valores de toopass para hello *ResourceGroupName* y *DataFactoryName* parámetros.</span><span class="sxs-lookup"><span data-stu-id="18811-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="18811-172">Como alternativa, puede usar **Get AzureRmDataFactory** tooget una **DataFactory** objeto y pasar el objeto de hello sin escribir *ResourceGroupName* y  *DataFactoryName* cada vez que ejecute un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18811-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="18811-173">Siguiente ejecución Hola comando salida de hello tooassign de hello **Get AzureRmDataFactory** cmdlet tooa **$df** variable.</span><span class="sxs-lookup"><span data-stu-id="18811-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="18811-174">Ahora, ejecute hello **New-AzureRmDataFactoryLinkedService** cmdlet que crea Hola vinculado **StorageLinkedService** servicio.</span><span class="sxs-lookup"><span data-stu-id="18811-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="18811-175">Si no se había ejecutado hello **Get AzureRmDataFactory** hello asignado y cmdlet de salida toohello **$df** variable, tendría toospecify valores de hello *ResourceGroupName*y *DataFactoryName* parámetros tal y como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="18811-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="18811-176">Si cierra Azure PowerShell en medio de Hola de tutorial de hello, tendrá que hello toorun **AzureRmDataFactory Get** cmdlet próxima vez que inicie el tutorial de Azure PowerShell toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="18811-177">Creación de un servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="18811-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="18811-178">En este paso, vincular un generador de datos a petición tooyour de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18811-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="18811-179">clúster de HDInsight de Hello automáticamente está creado en tiempo de ejecución y eliminar después de hacerlo inactivos y procesamiento para el período de tiempo especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="18811-180">Puede usar su propio clúster de HDInsight en lugar de usar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="18811-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="18811-181">Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="18811-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="18811-182">Cree un archivo JSON denominado **HDInsightOnDemandLinkedService**.json Hola **C:\ADFGetStarted** carpeta con hello siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="18811-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="18811-183">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="18811-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="18811-184">Propiedad</span><span class="sxs-lookup"><span data-stu-id="18811-184">Property</span></span> | <span data-ttu-id="18811-185">Descripción</span><span class="sxs-lookup"><span data-stu-id="18811-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="18811-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="18811-186">ClusterSize</span></span> |<span data-ttu-id="18811-187">Especifica el tamaño de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18811-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="18811-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="18811-188">TimeToLive</span></span> |<span data-ttu-id="18811-189">Especifica ese tiempo de inactividad de hello para el clúster de HDInsight de hello, antes de eliminarla.</span><span class="sxs-lookup"><span data-stu-id="18811-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="18811-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="18811-190">linkedServiceName</span></span> |<span data-ttu-id="18811-191">Especifica la cuenta de almacenamiento de Hola que es toostore usado Hola registros generados por HDInsight</span><span class="sxs-lookup"><span data-stu-id="18811-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="18811-192">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="18811-192">Note hello following points:</span></span>

   * <span data-ttu-id="18811-193">Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello JSON.</span><span class="sxs-lookup"><span data-stu-id="18811-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="18811-194">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="18811-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="18811-195">Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="18811-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="18811-196">Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="18811-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="18811-197">clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="18811-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="18811-198">HDInsight no elimine este contenedor cuando se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="18811-199">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="18811-199">This behavior is by design.</span></span> <span data-ttu-id="18811-200">Con el servicio vinculado de HDInsight a petición se crea un clúster de HDInsight cada vez se procesa un segmento, a menos que haya un clúster existente activo (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="18811-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="18811-201">clúster de Hola se elimina automáticamente cuando se realiza un procesamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="18811-202">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="18811-203">Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="18811-204">nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="18811-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="18811-205">Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="18811-206">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="18811-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="18811-207">Ejecute hello **AzureRmDataFactoryLinkedService New** cmdlet que crea Hola vinculado servicio denominado HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="18811-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="18811-208">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="18811-208">Create datasets</span></span>
<span data-ttu-id="18811-209">En este paso, creación de conjuntos de datos toorepresent Hola entrada y salida de datos para el procesamiento de Hive.</span><span class="sxs-lookup"><span data-stu-id="18811-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="18811-210">Estos conjuntos de datos, consulte toohello **StorageLinkedService** ha creado anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="18811-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="18811-211">Hola tooan de puntos de servicio vinculado cuenta de almacenamiento de Azure y los conjuntos de datos especifiquen contenedor, carpeta, nombre de archivo en el almacenamiento de Hola que contiene la entrada y salida de datos.</span><span class="sxs-lookup"><span data-stu-id="18811-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="18811-212">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="18811-212">Create input dataset</span></span>
1. <span data-ttu-id="18811-213">Cree un archivo JSON denominado **InputTable.json** en hello **C:\ADFGetStarted** carpeta con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="18811-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="18811-214">Hola JSON define un conjunto de datos denominado **AzureBlobInput**, que representa los datos de entrada para una actividad de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="18811-215">Además, especifica que los datos de entrada de Hola se encuentran en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="18811-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="18811-216">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="18811-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="18811-217">Propiedad</span><span class="sxs-lookup"><span data-stu-id="18811-217">Property</span></span> | <span data-ttu-id="18811-218">Descripción</span><span class="sxs-lookup"><span data-stu-id="18811-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="18811-219">type</span><span class="sxs-lookup"><span data-stu-id="18811-219">type</span></span> |<span data-ttu-id="18811-220">propiedad de tipo Hello se establece tooAzureBlob porque los datos residen en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="18811-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="18811-221">linkedServiceName</span></span> |<span data-ttu-id="18811-222">se refiere toohello StorageLinkedService que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="18811-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="18811-223">fileName</span><span class="sxs-lookup"><span data-stu-id="18811-223">fileName</span></span> |<span data-ttu-id="18811-224">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="18811-224">This property is optional.</span></span> <span data-ttu-id="18811-225">Si se omite esta propiedad, se seleccionan todos los archivos de Hola de hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="18811-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="18811-226">En este caso, se procesa solo hello input.log.</span><span class="sxs-lookup"><span data-stu-id="18811-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="18811-227">type</span><span class="sxs-lookup"><span data-stu-id="18811-227">type</span></span> |<span data-ttu-id="18811-228">archivos de registro de Hello están en formato de texto, por lo que usamos TextFormat.</span><span class="sxs-lookup"><span data-stu-id="18811-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="18811-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="18811-229">columnDelimiter</span></span> |<span data-ttu-id="18811-230">columnas en los archivos de registro de hello están delimitadas por caracteres de Hola por comas (,).</span><span class="sxs-lookup"><span data-stu-id="18811-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="18811-231">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="18811-231">frequency/interval</span></span> |<span data-ttu-id="18811-232">la frecuencia debe establecer tooMonth y interval es 1, lo que significa que están disponibles los segmentos de entrada de hello mensualmente.</span><span class="sxs-lookup"><span data-stu-id="18811-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="18811-233">external</span><span class="sxs-lookup"><span data-stu-id="18811-233">external</span></span> |<span data-ttu-id="18811-234">Esta propiedad se establece tootrue si servicio de factoría de datos de hello no genera datos de entrada de saludo.</span><span class="sxs-lookup"><span data-stu-id="18811-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="18811-235">Ejecute el siguiente comando en el conjunto de datos de Azure PowerShell toocreate Hola factoría de datos de Hola:</span><span class="sxs-lookup"><span data-stu-id="18811-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="18811-236">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="18811-236">Create output dataset</span></span>
<span data-ttu-id="18811-237">Ahora, cree Hola salida dataset toorepresent Hola salida datos almacenados en hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="18811-238">Cree un archivo JSON denominado **OutputTable.json** en hello **C:\ADFGetStarted** carpeta con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="18811-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="18811-239">Hola JSON define un conjunto de datos denominado **AzureBlobOutput**, que representa los datos de salida para una actividad de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="18811-240">Además, especifica que los resultados de Hola se almacenan en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="18811-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="18811-241">Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se genera mensualmente.</span><span class="sxs-lookup"><span data-stu-id="18811-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="18811-242">Ejecute el siguiente comando en el conjunto de datos de Azure PowerShell toocreate Hola factoría de datos de Hola:</span><span class="sxs-lookup"><span data-stu-id="18811-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="18811-243">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="18811-243">Create pipeline</span></span>
<span data-ttu-id="18811-244">En este paso, creará la primera canalización con una actividad **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="18811-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="18811-245">Segmento de entrada está disponible mensual (frecuencia: mes, intervalo: 1), segmento de salida se genera mensualmente y Hola programador propiedad actividad hello también está configurada toomonthly.</span><span class="sxs-lookup"><span data-stu-id="18811-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="18811-246">debe coincidir con la configuración de Hello para el conjunto de datos de salida de Hola y el programador de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="18811-247">Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="18811-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="18811-248">Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada.</span><span class="sxs-lookup"><span data-stu-id="18811-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="18811-249">propiedades de Hello utilizadas en hello después de JSON se explican al final de Hola de esta sección.</span><span class="sxs-lookup"><span data-stu-id="18811-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="18811-250">Cree un archivo JSON denominado MyFirstPipelinePSH.json en la carpeta de hello C:\ADFGetStarted con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="18811-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="18811-251">Reemplace **storageaccountname** con el nombre de Hola de su cuenta de almacenamiento en hello JSON.</span><span class="sxs-lookup"><span data-stu-id="18811-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
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
    <span data-ttu-id="18811-252">En el fragmento JSON de hello, desea crear una canalización que consta de una actividad única que usa Hive tooprocess datos en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18811-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="18811-253">archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **StorageLinkedService**) y en **secuencias de comandos**  carpeta en el contenedor de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="18811-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="18811-254">Hola **define** sección es configuración en tiempo de ejecución de toospecify usado Hola que ser pasa el script de hive toohello como valores de configuración de Hive (por ejemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="18811-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="18811-255">Hola **iniciar** y **final** propiedades de canalización de hello especifica el periodo activo de Hola de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="18811-256">En JSON de la actividad de hello, especifique ese script de Hive Hola se ejecuta en proceso Hola especificado por hello **linkedServiceName** : **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="18811-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="18811-257">Consulte la sección "JSON de canalización" en [canalizaciones y actividades de Data Factory de Azure](data-factory-create-pipelines.md) para obtener más información acerca de las propiedades JSON que se usan en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="18811-258">Confirme que aparece hello **input.log** archivo Hola **adfgetstarted/inputdata** carpeta Hola almacenamiento de blobs de Azure y ejecución Hola después de la canalización de comandos toodeploy Hola de.</span><span class="sxs-lookup"><span data-stu-id="18811-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="18811-259">Desde hello **iniciar** y **final** veces se establecen en los último hello y **isPaused** es toofalse de conjunto, canalización Hola ejecuciones (actividad de canalización de hello) inmediatamente después de implementar.</span><span class="sxs-lookup"><span data-stu-id="18811-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="18811-260">Enhorabuena, ya creó correctamente su primera canalización con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18811-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="18811-261">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="18811-261">Monitor pipeline</span></span>
<span data-ttu-id="18811-262">En este paso, utilice toomonitor de PowerShell de Azure que está sucediendo en una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="18811-263">Ejecutar **Get AzureRmDataFactory** y asignar Hola salida tooa **$df** variable.</span><span class="sxs-lookup"><span data-stu-id="18811-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="18811-264">Ejecutar **Get AzureRmDataFactorySlice** tooget obtener más información acerca de todos los sectores de hello **EmpSQLTable**, que es la tabla de salida de hello de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="18811-265">Tenga en cuenta que Hola StartDateTime que especifique aquí es hello que igual especificado en JSON de la canalización de Hola de hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="18811-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="18811-266">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="18811-266">Here is hello sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="18811-267">Ejecutar **AzureRmDataFactoryRun Get** tooget Hola detalles de actividad se ejecuta durante un determinado segmento.</span><span class="sxs-lookup"><span data-stu-id="18811-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="18811-268">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="18811-268">Here is hello sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="18811-269">Puede mantener ejecutar este cmdlet hasta que vea en el sector de hello **listo** estado o **error** estado.</span><span class="sxs-lookup"><span data-stu-id="18811-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="18811-270">Al segmento de hello está en estado listo, comprobar hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="18811-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="18811-271">La creación de un clúster de HDInsight a petición normalmente requiere algo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="18811-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![datos de salida](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="18811-273">La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="18811-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="18811-274">Por consiguiente, esperan Hola canalización tootake **aproximadamente 30 minutos** tooprocess Hola segmento.</span><span class="sxs-lookup"><span data-stu-id="18811-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="18811-275">archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente.</span><span class="sxs-lookup"><span data-stu-id="18811-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="18811-276">Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="18811-277">Resumen</span><span class="sxs-lookup"><span data-stu-id="18811-277">Summary</span></span>
<span data-ttu-id="18811-278">En este tutorial, ha creado un datos tooprocess de factoría de datos de Azure mediante la ejecución de script de Hive en un clúster de hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18811-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="18811-279">Utiliza el Editor de generador de datos de Hola Hola toodo portal Azure Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="18811-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="18811-280">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="18811-281">Ha creado dos **servicios vinculados**:</span><span class="sxs-lookup"><span data-stu-id="18811-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="18811-282">**Almacenamiento de Azure** vinculado servicio toolink el almacenamiento de blobs de Azure que contiene la factoría de datos de archivos de entrada/salida toohello.</span><span class="sxs-lookup"><span data-stu-id="18811-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="18811-283">**HDInsight de Azure** toolink de servicio vinculado a petición una factoría de datos a petición toohello de clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="18811-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="18811-284">Factoría de datos de Azure crea un Hadoop de HDInsight los datos de entrada de tooprocess just-in-time de clúster y generan datos de salida.</span><span class="sxs-lookup"><span data-stu-id="18811-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="18811-285">Crea dos **conjuntos de datos**, que describen los datos de entrada y salidos de actividad de Hive de HDInsight en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="18811-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="18811-286">Ha creado una **canalización** con una actividad de **Hive de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="18811-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18811-287">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18811-287">Next steps</span></span>
<span data-ttu-id="18811-288">En este artículo, creó una canalización con una actividad de transformación (actividad de HDInsight) que ejecuta un script de Hive en un clúster de HDInsight de Azure a petición.</span><span class="sxs-lookup"><span data-stu-id="18811-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="18811-289">toosee toouse una toocopy de datos de actividad de copia de un tooAzure de Blob de Azure SQL, vea [Tutorial: copiar los datos de un tooAzure de Blob de Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="18811-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="18811-290">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="18811-290">See Also</span></span>
| <span data-ttu-id="18811-291">Tema.</span><span class="sxs-lookup"><span data-stu-id="18811-291">Topic</span></span> | <span data-ttu-id="18811-292">Descripción</span><span class="sxs-lookup"><span data-stu-id="18811-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="18811-293">Referencia para cmdlets de Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="18811-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="18811-294">Consulte la documentación completa sobre los cmdlets de Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="18811-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="18811-295">Procesos</span><span class="sxs-lookup"><span data-stu-id="18811-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="18811-296">En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa.</span><span class="sxs-lookup"><span data-stu-id="18811-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="18811-297">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="18811-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="18811-298">Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="18811-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="18811-299">Programación y ejecución</span><span class="sxs-lookup"><span data-stu-id="18811-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="18811-300">En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="18811-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="18811-301">Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="18811-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="18811-302">Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="18811-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
