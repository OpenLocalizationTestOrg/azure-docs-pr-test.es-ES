---
title: "aaaBuild su primera factoría de datos (REST) | Documentos de Microsoft"
description: "En este tutorial se crea un ejemplo de canalización de Data Factory de Azure con la API de REST de Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="fea60-103">Tutorial: Compilación de la primera instancia de Azure Data Factory con la API de REST de Data Factory</span><span class="sxs-lookup"><span data-stu-id="fea60-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fea60-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fea60-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="fea60-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fea60-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="fea60-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fea60-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="fea60-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fea60-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="fea60-108">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fea60-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="fea60-109">API DE REST</span><span class="sxs-lookup"><span data-stu-id="fea60-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="fea60-110">En este artículo, use API de REST de factoría de datos toocreate su primera factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="fea60-111">tutorial de hello toodo mediante otra herramientas y SDK, seleccione una de las opciones de Hola de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="fea60-112">canalización de Hello en este tutorial tiene una actividad: **actividad de HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="fea60-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="fea60-113">Esta actividad ejecuta un script de hive en un clúster de HDInsight de Azure que las transformaciones de entrada de datos de salida de datos tooproduce.</span><span class="sxs-lookup"><span data-stu-id="fea60-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="fea60-114">canalización de Hello es toorun programado una vez que un mes entre Hola especificado horas de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="fea60-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="fea60-115">Este artículo no cubre Hola todas las API de REST.</span><span class="sxs-lookup"><span data-stu-id="fea60-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="fea60-116">Para obtener documentación completa sobre la API de REST, consulte la [referencia de la API de REST de Data Factory](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="fea60-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="fea60-117">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="fea60-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="fea60-118">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="fea60-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="fea60-119">Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="fea60-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fea60-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fea60-120">Prerequisites</span></span>
* <span data-ttu-id="fea60-121">Lea [Tutorial de introducción](data-factory-build-your-first-pipeline.md) hello completa y artículo **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="fea60-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="fea60-122">Instale [Curl](https://curl.haxx.se/dlwiz/) en su máquina.</span><span class="sxs-lookup"><span data-stu-id="fea60-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="fea60-123">Usar herramienta de hello CURL con REST comandos toocreate una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fea60-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="fea60-124">Siga las instrucciones de [este artículo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:</span><span class="sxs-lookup"><span data-stu-id="fea60-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="fea60-125">Cree una aplicación web denominada **ADFGetStartedApp** en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fea60-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="fea60-126">Obtenga el **Id. de cliente** y la **Clave secreta**.</span><span class="sxs-lookup"><span data-stu-id="fea60-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="fea60-127">Obtenga el **Identificador de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="fea60-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="fea60-128">Asignar Hola **ADFGetStartedApp** aplicación toohello **colaborador de la factoría de datos** rol.</span><span class="sxs-lookup"><span data-stu-id="fea60-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="fea60-129">Instale [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fea60-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fea60-130">Iniciar **PowerShell** y ejecución Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="fea60-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="fea60-131">Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fea60-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="fea60-132">Si cerrar y volver a abrir, se necesitan toorun comandos de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="fea60-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="fea60-133">Ejecutar **AzureRmAccount de inicio de sesión** y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="fea60-134">Ejecutar **AzureRmSubscription Get** tooview todos Hola suscripciones para esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="fea60-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="fea60-135">Ejecutar **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Conjunto AzureRmContext** suscripción de hello tooselect que desea toowork con.</span><span class="sxs-lookup"><span data-stu-id="fea60-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="fea60-136">Reemplace **NameOfAzureSubscription** con el nombre de Hola de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="fea60-137">Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando en hello PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fea60-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="fea60-138">Algunos de los pasos de hello en este tutorial se supone que usa el grupo de recursos de hello llamado ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="fea60-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="fea60-139">Si utiliza un grupo de recursos diferente, necesita toouse Hola nombre de su grupo de recursos en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fea60-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="fea60-140">Creación de definiciones de JSON</span><span class="sxs-lookup"><span data-stu-id="fea60-140">Create JSON definitions</span></span>
<span data-ttu-id="fea60-141">Crear siguientes archivos JSON en carpeta Hola donde se encuentra curl.exe.</span><span class="sxs-lookup"><span data-stu-id="fea60-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="fea60-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="fea60-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fea60-143">Nombre debe ser único globalmente, por lo que puede tooprefix/sufijo ADFCopyTutorialDF toomake, un nombre único.</span><span class="sxs-lookup"><span data-stu-id="fea60-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="fea60-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="fea60-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fea60-145">Reemplace **accountname** y **accountkey** por el nombre y la clave de su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="fea60-146">toolearn el proceso tooget el almacenamiento de acceso de clave, vea Hola información acerca de cómo tooview, copiar y regenerar almacenamiento tener acceso a claves de [administrar su cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fea60-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

```JSON
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="fea60-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="fea60-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="fea60-148">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="fea60-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="fea60-149">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fea60-149">Property</span></span> | <span data-ttu-id="fea60-150">Descripción</span><span class="sxs-lookup"><span data-stu-id="fea60-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fea60-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="fea60-151">ClusterSize</span></span> |<span data-ttu-id="fea60-152">Tamaño de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="fea60-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="fea60-153">TimeToLive</span></span> |<span data-ttu-id="fea60-154">Especifica ese tiempo de inactividad de hello para el clúster de HDInsight de hello, antes de eliminarla.</span><span class="sxs-lookup"><span data-stu-id="fea60-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="fea60-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fea60-155">linkedServiceName</span></span> |<span data-ttu-id="fea60-156">Especifica la cuenta de almacenamiento de Hola que es toostore usado Hola registros generados por HDInsight</span><span class="sxs-lookup"><span data-stu-id="fea60-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="fea60-157">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="fea60-157">Note hello following points:</span></span>

* <span data-ttu-id="fea60-158">Hello factoría de datos se crea un **basados en Linux** clúster de HDInsight automáticamente con hello por encima de JSON.</span><span class="sxs-lookup"><span data-stu-id="fea60-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="fea60-159">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="fea60-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="fea60-160">Puede usar **su propio clúster de HDInsight** en lugar de usar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="fea60-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fea60-161">Para más información, consulte [Servicio vinculado de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="fea60-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="fea60-162">clúster de HDInsight de Hello crea un **contenedor predeterminado** en almacenamiento de blobs de Hola que especificó en hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="fea60-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="fea60-163">HDInsight no elimine este contenedor cuando se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="fea60-164">Este comportamiento es así por diseño.</span><span class="sxs-lookup"><span data-stu-id="fea60-164">This behavior is by design.</span></span> <span data-ttu-id="fea60-165">Con el servicio de vinculado de HDInsight a petición, se crea un clúster de HDInsight cada vez que se procesa un segmento a menos que haya un clúster existente en vivo (**timeToLive**) y se elimina cuando se realiza un procesamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="fea60-166">A medida que se procesen más segmentos, verá numerosos contenedores en su Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="fea60-167">Si no se necesita para solucionar problemas de trabajos de hello, quizá le interese toodelete ellos el costo de almacenamiento de tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="fea60-168">nombres de Hola de estos contenedores siguen un patrón: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="fea60-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="fea60-169">Usar herramientas como [Explorador de almacenamiento de Microsoft](http://storageexplorer.com/) almacenamiento de blobs de contenedores de toodelete en Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="fea60-170">Para más información, consulte la sección [Servicio vinculado a petición de HDInsight de Azure](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) .</span><span class="sxs-lookup"><span data-stu-id="fea60-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="fea60-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="fea60-171">inputdataset.json</span></span>

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

<span data-ttu-id="fea60-172">Hola JSON define un conjunto de datos denominado **AzureBlobInput**, que representa los datos de entrada para una actividad de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="fea60-173">Además, especifica que los datos de entrada de Hola se encuentran en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="fea60-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="fea60-174">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="fea60-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="fea60-175">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fea60-175">Property</span></span> | <span data-ttu-id="fea60-176">Descripción</span><span class="sxs-lookup"><span data-stu-id="fea60-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fea60-177">type</span><span class="sxs-lookup"><span data-stu-id="fea60-177">type</span></span> |<span data-ttu-id="fea60-178">propiedad de tipo Hello se establece tooAzureBlob porque los datos residen en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="fea60-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fea60-179">linkedServiceName</span></span> |<span data-ttu-id="fea60-180">se refiere toohello StorageLinkedService que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fea60-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="fea60-181">fileName</span><span class="sxs-lookup"><span data-stu-id="fea60-181">fileName</span></span> |<span data-ttu-id="fea60-182">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="fea60-182">This property is optional.</span></span> <span data-ttu-id="fea60-183">Si se omite esta propiedad, se seleccionan todos los archivos de Hola de hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="fea60-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="fea60-184">En este caso, se procesa solo hello input.log.</span><span class="sxs-lookup"><span data-stu-id="fea60-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="fea60-185">type</span><span class="sxs-lookup"><span data-stu-id="fea60-185">type</span></span> |<span data-ttu-id="fea60-186">archivos de registro de Hello están en formato de texto, por lo que usamos TextFormat.</span><span class="sxs-lookup"><span data-stu-id="fea60-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="fea60-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="fea60-187">columnDelimiter</span></span> |<span data-ttu-id="fea60-188">las columnas en los archivos de registro de hello se delimitan por un carácter de coma ()</span><span class="sxs-lookup"><span data-stu-id="fea60-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="fea60-189">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="fea60-189">frequency/interval</span></span> |<span data-ttu-id="fea60-190">la frecuencia debe establecer tooMonth y interval es 1, lo que significa que están disponibles los segmentos de entrada de hello mensualmente.</span><span class="sxs-lookup"><span data-stu-id="fea60-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="fea60-191">external</span><span class="sxs-lookup"><span data-stu-id="fea60-191">external</span></span> |<span data-ttu-id="fea60-192">Esta propiedad se establece tootrue si servicio de factoría de datos de hello no genera datos de entrada de saludo.</span><span class="sxs-lookup"><span data-stu-id="fea60-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="fea60-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="fea60-193">outputdataset.json</span></span>

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

<span data-ttu-id="fea60-194">Hola JSON define un conjunto de datos denominado **AzureBlobOutput**, que representa los datos de salida para una actividad de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="fea60-195">Además, especifica que los resultados de Hola se almacenan en contenedor de blob de hello denominado **adfgetstarted** y carpeta Hola llamada **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="fea60-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="fea60-196">Hola **disponibilidad** sección especifica ese conjunto de datos de salida de hello se genera mensualmente.</span><span class="sxs-lookup"><span data-stu-id="fea60-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="fea60-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="fea60-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fea60-198">Reemplace **storageaccountname** por el nombre de la cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="fea60-199">En el fragmento JSON de hello, desea crear una canalización que consta de una actividad única que usa datos de tooprocess de Hive en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fea60-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="fea60-200">archivo de script de Hive de Hello, **partitionweblogs.hql**, se almacena en hello cuenta de almacenamiento de Azure (especificado por scriptLinkedService hello, denominado **StorageLinkedService**) y en **secuencias de comandos**  carpeta en el contenedor de hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="fea60-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="fea60-201">Hola **define** sección especifica los valores de tiempo de ejecución que se pasan el script de hive toohello como valores de configuración de Hive (por ejemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="fea60-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="fea60-202">Hola **iniciar** y **final** propiedades de canalización de hello especifica el periodo activo de Hola de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="fea60-203">En JSON de la actividad de hello, especifique ese script de Hive Hola se ejecuta en proceso Hola especificado por hello **linkedServiceName** : **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="fea60-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="fea60-204">Consulte la sección "JSON de canalización" en [canalizaciones y actividades de Data Factory de Azure](data-factory-create-pipelines.md) para obtener más información sobre propiedades JSON que se usan en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="fea60-205">Definición de variables globales</span><span class="sxs-lookup"><span data-stu-id="fea60-205">Set global variables</span></span>
<span data-ttu-id="fea60-206">En Azure PowerShell, ejecute hello después de comandos después de reemplazar los valores de hello con su propio:</span><span class="sxs-lookup"><span data-stu-id="fea60-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fea60-207">Consulte la sección [Requisitos previos](#prerequisites) para obtener instrucciones sobre cómo obtener el identificador de cliente, el secreto del cliente, el identificador de inquilino y el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="fea60-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="fea60-208">Autenticación con AAD</span><span class="sxs-lookup"><span data-stu-id="fea60-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="fea60-209">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="fea60-209">Create data factory</span></span>
<span data-ttu-id="fea60-210">En este paso, creará una instancia de Data Factory de Azure llamada **LogProcessingFactory**.</span><span class="sxs-lookup"><span data-stu-id="fea60-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="fea60-211">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="fea60-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="fea60-212">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="fea60-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="fea60-213">Por ejemplo, una actividad de copia toocopy datos de un almacén de datos de origen tooa destino y un toorun de actividad de Hive de HDInsight una tootransform de datos de script de Hive.</span><span class="sxs-lookup"><span data-stu-id="fea60-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="fea60-214">Ejecute hello después de la factoría de datos de comandos toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="fea60-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="fea60-215">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fea60-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="fea60-216">Confirmar ese nombre Hola Hola factoría de datos que especifique aquí (ADFCopyTutorialDF) coincidencias Hola nombre especificado en hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="fea60-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fea60-217">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fea60-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fea60-218">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-218">View hello results.</span></span> <span data-ttu-id="fea60-219">Si se ha creado correctamente la factoría de datos de hello, vea Hola JSON de factoría de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="fea60-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="fea60-220">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="fea60-220">Note hello following points:</span></span>

* <span data-ttu-id="fea60-221">nombre de Hola de hello Data Factory de Azure debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="fea60-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="fea60-222">Si ve errores de hello en los resultados: **nombre de generador de datos "FirstDataFactoryREST" no está disponible**, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fea60-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="fea60-223">Cambiar el nombre de hello (por ejemplo, yournameFirstDataFactoryREST) en hello **datafactory.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="fea60-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="fea60-224">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="fea60-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="fea60-225">En el primer comando de Hola Hola donde **$cmd** se asigna un valor variable, reemplace FirstDataFactoryREST con el nombre nuevo de Hola y ejecute el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="fea60-226">Resultados de la ejecución toocreate de API de REST de hello dos comandos siguientes tooinvoke Hola Hola datos generador e impresión Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="fea60-227">instancias de la factoría de datos de toocreate, deberá toobe un colaborador o administrador de hello suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="fea60-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="fea60-228">nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, están visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="fea60-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="fea60-229">Si recibe el error hello: "**esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory**", siga uno de los procedimientos de Hola e intente publicar de nuevo:</span><span class="sxs-lookup"><span data-stu-id="fea60-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="fea60-230">En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="fea60-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="fea60-231">Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado:</span><span class="sxs-lookup"><span data-stu-id="fea60-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="fea60-232">Inicio de sesión mediante Hola suscripción de Azure en hello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="fea60-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="fea60-233">Esta acción registra automáticamente proveedor Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="fea60-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="fea60-234">Antes de crear una canalización, necesita toocreate algunas entidades de la factoría de datos en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="fea60-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="fea60-235">En primer lugar crear datos de servicios vinculados toolink almacenes/calcula tooyour y almacén de datos, definen una entrada generar conjuntos de datos toorepresent datos en almacenes de datos vinculado.</span><span class="sxs-lookup"><span data-stu-id="fea60-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="fea60-236">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="fea60-236">Create linked services</span></span>
<span data-ttu-id="fea60-237">En este paso, vincular su cuenta de almacenamiento de Azure y un generador de datos a petición tooyour de clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="fea60-238">Hola cuenta de almacenamiento de Azure que contiene datos de entrada y salidas de la canalización de hello en este ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="fea60-239">Hola servicio vinculado de HDInsight es toorun usa un script de Hive especificado en la actividad de hello de canalización de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fea60-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="fea60-240">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="fea60-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="fea60-241">En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="fea60-242">Con este tutorial, utilice Hola misma cuenta de almacenamiento de Azure hello HQL y datos de entrada/salida de toostore los archivos de scripts.</span><span class="sxs-lookup"><span data-stu-id="fea60-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="fea60-243">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fea60-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fea60-244">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fea60-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fea60-245">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-245">View hello results.</span></span> <span data-ttu-id="fea60-246">Si Hola vinculado se ha creado correctamente el servicio, vea Hola JSON para el servicio de hello vinculado en hello **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="fea60-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="fea60-247">Creación de un servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="fea60-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="fea60-248">En este paso, vincular un generador de datos a petición tooyour de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fea60-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="fea60-249">clúster de HDInsight de Hello automáticamente está creado en tiempo de ejecución y eliminar después de hacerlo inactivos y procesamiento para el período de tiempo especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="fea60-250">Puede usar su propio clúster de HDInsight en lugar de usar un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="fea60-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fea60-251">Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="fea60-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="fea60-252">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fea60-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fea60-253">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fea60-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fea60-254">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-254">View hello results.</span></span> <span data-ttu-id="fea60-255">Si Hola vinculado se ha creado correctamente el servicio, vea Hola JSON para el servicio de hello vinculado en hello **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="fea60-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="fea60-256">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="fea60-256">Create datasets</span></span>
<span data-ttu-id="fea60-257">En este paso, creación de conjuntos de datos toorepresent Hola entrada y salida de datos para el procesamiento de Hive.</span><span class="sxs-lookup"><span data-stu-id="fea60-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="fea60-258">Estos conjuntos de datos, consulte toohello **StorageLinkedService** ha creado anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fea60-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="fea60-259">Hola tooan de puntos de servicio vinculado cuenta de almacenamiento de Azure y los conjuntos de datos especifiquen contenedor, carpeta, nombre de archivo en el almacenamiento de Hola que contiene la entrada y salida de datos.</span><span class="sxs-lookup"><span data-stu-id="fea60-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="fea60-260">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="fea60-260">Create input dataset</span></span>
<span data-ttu-id="fea60-261">En este paso, creará Hola conjunto de datos de entrada toorepresent entrada los datos almacenados en almacenamiento de blobs de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="fea60-262">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fea60-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fea60-263">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fea60-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fea60-264">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-264">View hello results.</span></span> <span data-ttu-id="fea60-265">Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="fea60-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="fea60-266">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="fea60-266">Create output dataset</span></span>
<span data-ttu-id="fea60-267">En este paso, creará Hola salida dataset toorepresent salida los datos almacenados en hello almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="fea60-268">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fea60-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fea60-269">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fea60-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fea60-270">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-270">View hello results.</span></span> <span data-ttu-id="fea60-271">Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="fea60-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="fea60-272">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="fea60-272">Create pipeline</span></span>
<span data-ttu-id="fea60-273">En este paso, creará la primera canalización con una actividad **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="fea60-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="fea60-274">Segmento de entrada está disponible mensual (frecuencia: mes, intervalo: 1), segmento de salida se genera mensualmente y Hola programador propiedad actividad hello también está configurada toomonthly.</span><span class="sxs-lookup"><span data-stu-id="fea60-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="fea60-275">debe coincidir con la configuración de Hello para el conjunto de datos de salida de Hola y el programador de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="fea60-276">Actualmente, el conjunto de datos de salida es qué unidades Hola programación, por lo que debe crear un conjunto de datos de salida aunque actividad hello no genera ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="fea60-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="fea60-277">Si la actividad hello no toma ninguna entrada, puede omitir creación Hola de conjunto de datos entrada.</span><span class="sxs-lookup"><span data-stu-id="fea60-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="fea60-278">Confirme que aparece hello **input.log** archivo Hola **adfgetstarted/inputdata** carpeta Hola almacenamiento de blobs de Azure y ejecución Hola después de la canalización de comandos toodeploy Hola de.</span><span class="sxs-lookup"><span data-stu-id="fea60-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="fea60-279">Desde hello **iniciar** y **final** veces se establecen en los último hello y **isPaused** es toofalse de conjunto, canalización Hola ejecuciones (actividad de canalización de hello) inmediatamente después de implementar.</span><span class="sxs-lookup"><span data-stu-id="fea60-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="fea60-280">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fea60-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fea60-281">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fea60-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fea60-282">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-282">View hello results.</span></span> <span data-ttu-id="fea60-283">Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="fea60-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="fea60-284">Enhorabuena, ya creó correctamente su primera canalización con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fea60-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="fea60-285">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="fea60-285">Monitor pipeline</span></span>
<span data-ttu-id="fea60-286">En este paso, utilice sectores de toomonitor de API de REST de factoría de datos se está generados en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="fea60-287">La creación de un clúster de HDInsight a petición normalmente tarda algún tiempo (20 minutos aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="fea60-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="fea60-288">Por consiguiente, esperan Hola canalización tootake **aproximadamente 30 minutos** tooprocess Hola segmento.</span><span class="sxs-lookup"><span data-stu-id="fea60-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="fea60-289">Ejecute Invoke-Command Hola y Hola siguiente hasta que vea sector hello en **listo** estado o **error** estado.</span><span class="sxs-lookup"><span data-stu-id="fea60-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="fea60-290">Al segmento de hello está en estado listo, comprobar hello **partitioneddata** carpeta Hola **adfgetstarted** contenedor en el almacenamiento de blobs para hello los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="fea60-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="fea60-291">creación de Hello de un clúster de HDInsight a petición normalmente tarda algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="fea60-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![datos de salida](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="fea60-293">archivo de entrada de Hola se elimina al segmento de Hola se procesa correctamente.</span><span class="sxs-lookup"><span data-stu-id="fea60-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="fea60-294">Por lo tanto, si desea toorerun Hola sector u Hola tutorial nuevo, cargar toohello inputdata carpeta de hello archivo de entrada (input.log) del contenedor de adfgetstarted Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="fea60-295">También puede utilizar Azure toomonitor portal sectores y solucione cualquier problema.</span><span class="sxs-lookup"><span data-stu-id="fea60-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="fea60-296">Consulte más detalles en la sección sobre la [supervisión de canalizaciones con el Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="fea60-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="fea60-297">Resumen</span><span class="sxs-lookup"><span data-stu-id="fea60-297">Summary</span></span>
<span data-ttu-id="fea60-298">En este tutorial, ha creado un datos tooprocess de factoría de datos de Azure mediante la ejecución de script de Hive en un clúster de hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fea60-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="fea60-299">Utiliza el Editor de generador de datos de Hola Hola toodo portal Azure Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="fea60-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="fea60-300">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="fea60-301">Ha creado dos **servicios vinculados**:</span><span class="sxs-lookup"><span data-stu-id="fea60-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="fea60-302">**Almacenamiento de Azure** vinculado servicio toolink el almacenamiento de blobs de Azure que contiene la factoría de datos de archivos de entrada/salida toohello.</span><span class="sxs-lookup"><span data-stu-id="fea60-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="fea60-303">**HDInsight de Azure** toolink de servicio vinculado a petición una factoría de datos a petición toohello de clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fea60-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="fea60-304">Factoría de datos de Azure crea un Hadoop de HDInsight los datos de entrada de tooprocess just-in-time de clúster y generan datos de salida.</span><span class="sxs-lookup"><span data-stu-id="fea60-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="fea60-305">Crea dos **conjuntos de datos**, que describen los datos de entrada y salidos de actividad de Hive de HDInsight en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea60-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="fea60-306">Ha creado una **canalización** con una actividad de **Hive de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fea60-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fea60-307">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fea60-307">Next steps</span></span>
<span data-ttu-id="fea60-308">En este artículo, creó una canalización con una actividad de transformación (actividad de HDInsight) que ejecuta un script de Hive en un clúster de HDInsight de Azure a petición.</span><span class="sxs-lookup"><span data-stu-id="fea60-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="fea60-309">toosee toouse una toocopy de datos de actividad de copia de un tooAzure de Blob de Azure SQL, vea [Tutorial: copiar los datos de un tooAzure de Blob de Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="fea60-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fea60-310">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="fea60-310">See Also</span></span>
| <span data-ttu-id="fea60-311">Tema.</span><span class="sxs-lookup"><span data-stu-id="fea60-311">Topic</span></span> | <span data-ttu-id="fea60-312">Descripción</span><span class="sxs-lookup"><span data-stu-id="fea60-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="fea60-313">Referencia de API de REST de Data Factory</span><span class="sxs-lookup"><span data-stu-id="fea60-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="fea60-314">Consulte la documentación completa sobre los cmdlets de Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="fea60-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="fea60-315">Procesos</span><span class="sxs-lookup"><span data-stu-id="fea60-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="fea60-316">En este artículo le ayudará a comprender las canalizaciones y actividades de Data Factory de Azure y cómo toouse les tooconstruct-to-end orientadas a datos los flujos de trabajo para su escenario o una empresa.</span><span class="sxs-lookup"><span data-stu-id="fea60-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="fea60-317">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="fea60-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="fea60-318">Este artículo le ayuda a comprender los conjuntos de datos de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea60-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="fea60-319">Programación y ejecución</span><span class="sxs-lookup"><span data-stu-id="fea60-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="fea60-320">En este artículo se explica los aspectos de programación y la ejecución de hello Data Factory de Azure del modelo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="fea60-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="fea60-321">Supervisión y administración de canalizaciones de Data Factory de Azure mediante la nueva Aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="fea60-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="fea60-322">Este artículo describe cómo administrar toomonitor y depurar las canalizaciones utilizando Hola supervisión y administración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fea60-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
