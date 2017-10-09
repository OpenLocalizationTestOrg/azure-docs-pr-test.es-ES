---
title: "Tutorial: Use la API de REST toocreate una canalización del generador de datos de Azure | Documentos de Microsoft"
description: "En este tutorial, use API de REST toocreate una canalización del generador de datos de Azure con una toocopy de datos de actividad de copia desde un almacenamiento de blobs de Azure una base de datos de SQL Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="9197f-103">Tutorial: Use la API de REST toocreate un toocopy de datos de canalización de factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="9197f-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9197f-104">Introducción y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9197f-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9197f-105">Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="9197f-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9197f-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9197f-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9197f-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9197f-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9197f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9197f-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9197f-109">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9197f-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9197f-110">API DE REST</span><span class="sxs-lookup"><span data-stu-id="9197f-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9197f-111">API de .NET</span><span class="sxs-lookup"><span data-stu-id="9197f-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="9197f-112">En este artículo, aprenderá cómo toouse REST API toocreate una factoría de datos con una canalización que copia datos de una base de datos de SQL Azure del tooan de almacenamiento blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="9197f-113">Si es nuevo tooAzure factoría de datos, lea hello [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo antes de realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9197f-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="9197f-114">En este tutorial, creará una canalización con una actividad en ella: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="9197f-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="9197f-115">actividad de copia de Hello copia datos de un almacén de datos de datos admitidos almacén tooa receptor admitidos.</span><span class="sxs-lookup"><span data-stu-id="9197f-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="9197f-116">Para obtener una lista de almacenes de datos que se admiten como orígenes y receptores, consulte los [almacenes de datos admitidos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9197f-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9197f-117">actividad Hello funciona con un servicio disponible globalmente que puede copiar datos entre varios almacenes de datos de forma segura, confiable y escalable.</span><span class="sxs-lookup"><span data-stu-id="9197f-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="9197f-118">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="9197f-119">pero cualquier canalización puede tener más de una actividad.</span><span class="sxs-lookup"><span data-stu-id="9197f-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="9197f-120">Y se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad.</span><span class="sxs-lookup"><span data-stu-id="9197f-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="9197f-121">Para más información, consulte [Varias actividades en una canalización](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="9197f-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="9197f-122">Este artículo no cubre Hola todas las API de REST de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="9197f-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="9197f-123">Consulte [Referencia de API de REST de Data Factory](/rest/api/datafactory/) para ver la documentación completa sobre los cmdlets de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9197f-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="9197f-124">canalización de datos de Hello en este tutorial copia datos de un almacén de datos de destino de origen datos almacén tooa.</span><span class="sxs-lookup"><span data-stu-id="9197f-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="9197f-125">Para obtener un tutorial sobre cómo tootransform los datos mediante Data Factory de Azure, consulte [Tutorial: generar una canalización de datos tootransform con clúster de Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9197f-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9197f-126">Prerequisites</span></span>
* <span data-ttu-id="9197f-127">Vaya a través de [Tutorial Introducción](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hello completa y **prerequisite** pasos.</span><span class="sxs-lookup"><span data-stu-id="9197f-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="9197f-128">Instale [Curl](https://curl.haxx.se/dlwiz/) en su máquina.</span><span class="sxs-lookup"><span data-stu-id="9197f-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="9197f-129">Usar herramienta de hello Curl con REST comandos toocreate una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="9197f-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="9197f-130">Siga las instrucciones de [este artículo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:</span><span class="sxs-lookup"><span data-stu-id="9197f-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="9197f-131">Cree una aplicación web denominada **ADFCopyTutorialApp** en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9197f-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="9197f-132">Obtenga el **Id. de cliente** y la **Clave secreta**.</span><span class="sxs-lookup"><span data-stu-id="9197f-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="9197f-133">Obtenga el **Identificador de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="9197f-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="9197f-134">Asignar Hola **ADFCopyTutorialApp** aplicación toohello **colaborador de la factoría de datos** rol.</span><span class="sxs-lookup"><span data-stu-id="9197f-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="9197f-135">Instale [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9197f-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="9197f-136">Iniciar **PowerShell** y Hola lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9197f-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="9197f-137">Mantenga Azure PowerShell abierta hasta final de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9197f-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="9197f-138">Si cerrar y volver a abrir, se necesitan toorun comandos de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="9197f-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="9197f-139">Ejecute el siguiente comando de Hola y escriba el nombre de usuario de Hola y la contraseña que usa toosign en toohello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="9197f-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="9197f-140">Ejecute hello después comando tooview todas las suscripciones de Hola para esta cuenta:</span><span class="sxs-lookup"><span data-stu-id="9197f-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="9197f-141">Ejecute hello después de suscripción de hello tooselect de comando que desee toowork con.</span><span class="sxs-lookup"><span data-stu-id="9197f-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="9197f-142">Reemplace  **&lt;NameOfAzureSubscription** &gt; con el nombre de Hola de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="9197f-143">Crear un grupo de recursos de Azure denominado **ADFTutorialResourceGroup** ejecutando Hola siguiente comando en hello PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9197f-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="9197f-144">Si ya existe el grupo de recursos de hello, especifique si tooupdate se (Y) o mantener un nivel tan (N).</span><span class="sxs-lookup"><span data-stu-id="9197f-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="9197f-145">Algunos de los pasos de hello en este tutorial se supone que usa el grupo de recursos de hello llamado ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="9197f-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="9197f-146">Si utiliza un grupo de recursos diferente, necesita toouse Hola nombre de su grupo de recursos en lugar de ADFTutorialResourceGroup en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9197f-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="9197f-147">Creación de definiciones de JSON</span><span class="sxs-lookup"><span data-stu-id="9197f-147">Create JSON definitions</span></span>
<span data-ttu-id="9197f-148">Crear siguientes archivos JSON en carpeta Hola donde se encuentra curl.exe.</span><span class="sxs-lookup"><span data-stu-id="9197f-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="9197f-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="9197f-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9197f-150">Nombre debe ser único globalmente, por lo que puede tooprefix/sufijo ADFCopyTutorialDF toomake, un nombre único.</span><span class="sxs-lookup"><span data-stu-id="9197f-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="9197f-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="9197f-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9197f-152">Reemplace **accountname** y **accountkey** por el nombre y la clave de su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="9197f-153">toolearn cómo tooget el almacenamiento de tener acceso a clave, consulte [ver, copiar y regenerar almacenamiento de claves de acceso](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="9197f-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="9197f-154">Para más información acerca de las propiedades JSON, consulte [servicio vinculado Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="9197f-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="9197f-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="9197f-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9197f-156">Reemplace **servername**, **databasename**, **nombre de usuario**, y **contraseña** con el nombre del servidor SQL Azure, nombre de base de datos SQL, usuario cuenta y contraseña de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="9197f-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="9197f-157">Para más información acerca de las propiedades JSON, consulte [servicio vinculado Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9197f-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="9197f-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="9197f-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
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
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
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

<span data-ttu-id="9197f-159">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="9197f-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="9197f-160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9197f-160">Property</span></span> | <span data-ttu-id="9197f-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="9197f-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9197f-162">type</span><span class="sxs-lookup"><span data-stu-id="9197f-162">type</span></span> | <span data-ttu-id="9197f-163">propiedad de tipo Hello se establece demasiado**AzureBlob** porque los datos residen en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="9197f-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9197f-164">linkedServiceName</span></span> | <span data-ttu-id="9197f-165">Hace referencia a toohello **AzureStorageLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9197f-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="9197f-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="9197f-166">folderPath</span></span> | <span data-ttu-id="9197f-167">Especifica el blob de hello **contenedor** hello y **carpeta** que contiene la entrada de blobs.</span><span class="sxs-lookup"><span data-stu-id="9197f-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="9197f-168">En este tutorial, adftutorial es el contenedor de blob de Hola y carpeta es la carpeta raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="9197f-169">fileName</span><span class="sxs-lookup"><span data-stu-id="9197f-169">fileName</span></span> | <span data-ttu-id="9197f-170">Esta propiedad es opcional.</span><span class="sxs-lookup"><span data-stu-id="9197f-170">This property is optional.</span></span> <span data-ttu-id="9197f-171">Si se omite esta propiedad, se seleccionan todos los archivos de hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="9197f-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="9197f-172">En este tutorial, **emp.txt** se especificó para hello nombre de archivo, por lo que sólo ese archivo se recoge para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="9197f-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="9197f-173">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="9197f-173">format -> type</span></span> |<span data-ttu-id="9197f-174">archivo de entrada de Hello es hello en formato de texto, por lo que usamos **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="9197f-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="9197f-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="9197f-175">columnDelimiter</span></span> | <span data-ttu-id="9197f-176">columnas de Hello en el archivo de entrada de Hola se delimitan mediante **carácter de coma (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="9197f-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="9197f-177">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="9197f-177">frequency/interval</span></span> | <span data-ttu-id="9197f-178">frecuencia de Hola se establece demasiado**hora** e intervalo está establecido demasiado**1**, lo que significa que Hola entrada sectores están disponibles **cada hora**.</span><span class="sxs-lookup"><span data-stu-id="9197f-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="9197f-179">En otras palabras, Hola servicio Data Factory busca datos de entrada cada hora en carpeta de raíz de hello del contenedor de blobs (**adftutorial**) que especificó.</span><span class="sxs-lookup"><span data-stu-id="9197f-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="9197f-180">Busca datos Hola Hola canalización inicio y finalización horas, no antes o después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="9197f-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="9197f-181">external</span><span class="sxs-lookup"><span data-stu-id="9197f-181">external</span></span> | <span data-ttu-id="9197f-182">Esta propiedad se establece demasiado**true** si no se generan datos de hello esta canalización.</span><span class="sxs-lookup"><span data-stu-id="9197f-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="9197f-183">datos de entrada de Hello en este tutorial están en el archivo emp.txt de hello, que no se genera esta canalización, por lo que se establece esta propiedad tootrue.</span><span class="sxs-lookup"><span data-stu-id="9197f-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="9197f-184">Para más información acerca de estas propiedades JSON, consulte el [artículo sobre el conector de blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9197f-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="9197f-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="9197f-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
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
<span data-ttu-id="9197f-186">Hello siguiente tabla proporciona descripciones de las propiedades JSON de hello utilizados en el fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="9197f-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="9197f-187">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9197f-187">Property</span></span> | <span data-ttu-id="9197f-188">Descripción</span><span class="sxs-lookup"><span data-stu-id="9197f-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9197f-189">type</span><span class="sxs-lookup"><span data-stu-id="9197f-189">type</span></span> | <span data-ttu-id="9197f-190">propiedad de tipo Hello se establece demasiado**AzureSqlTable** porque datos están la tabla de tooa copiado en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="9197f-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9197f-191">linkedServiceName</span></span> | <span data-ttu-id="9197f-192">Hace referencia a toohello **AzureSqlLinkedService** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9197f-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="9197f-193">tableName</span><span class="sxs-lookup"><span data-stu-id="9197f-193">tableName</span></span> | <span data-ttu-id="9197f-194">Hola especificado **tabla** toowhich Hola datos se copian.</span><span class="sxs-lookup"><span data-stu-id="9197f-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="9197f-195">frecuencia/intervalo</span><span class="sxs-lookup"><span data-stu-id="9197f-195">frequency/interval</span></span> | <span data-ttu-id="9197f-196">Hello frecuencia se establece demasiado**hora** y el intervalo es **1**, lo que significa que se producen los sectores de salida de hello **cada hora** entre el inicio de la canalización de Hola y de finalización veces, no antes o Después de esas horas.</span><span class="sxs-lookup"><span data-stu-id="9197f-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="9197f-197">Hay tres columnas: **identificador**, **FirstName**, y **LastName** : en la tabla emp de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="9197f-198">Id. es una columna de identidad, por lo que necesita solo toospecify **FirstName** y **LastName** aquí.</span><span class="sxs-lookup"><span data-stu-id="9197f-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="9197f-199">Para más información acerca de estas propiedades JSON, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9197f-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="9197f-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="9197f-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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

<span data-ttu-id="9197f-201">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="9197f-201">Note hello following points:</span></span>

- <span data-ttu-id="9197f-202">En la sección de actividades de hello, hay sólo una actividad cuyo **tipo** se establece demasiado**copia**.</span><span class="sxs-lookup"><span data-stu-id="9197f-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="9197f-203">Para obtener más información acerca de la actividad de copia de hello, consulte [las actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9197f-204">En las soluciones de Data Factory, también puede usar [actividades de transformación de datos](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="9197f-205">Entrada de actividad hello se establece demasiado**AzureBlobInput** y salida de actividad hello se establece demasiado**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="9197f-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="9197f-206">Hola **typeProperties** sección, **BlobSource** se especifica como tipo de origen de Hola y **SqlSink** se especifica como el tipo de receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="9197f-207">Para obtener una lista completa de los almacenes de datos compatibles con la actividad de copia de hello como orígenes y receptores, vea [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9197f-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9197f-208">toolearn cómo almacenar toouse datos compatibles especificados como un origen/receptor, haga clic en el vínculo hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="9197f-209">Reemplazar el valor de Hola de hello **iniciar** propiedad con hello día actual y **final** valor con hello día siguiente.</span><span class="sxs-lookup"><span data-stu-id="9197f-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="9197f-210">Puede especificar sólo parte de fecha de Hola y omitir la parte de hora de Hola de hello fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="9197f-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="9197f-211">Por ejemplo, "2017-02-03", que es equivalente demasiado "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="9197f-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="9197f-212">Las fechas y horas de inicio y de finalización deben estar en [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="9197f-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="9197f-213">Por ejemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="9197f-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="9197f-214">Hola **final** tiempo es opcional, pero se usa en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9197f-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="9197f-215">Si no especifica el valor de hello **final** propiedad, se calcula como "**inicio + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="9197f-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="9197f-216">canalización de hello toorun indefinidamente, especifique **9999-09-09** como valor de Hola de hello **final** propiedad.</span><span class="sxs-lookup"><span data-stu-id="9197f-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="9197f-217">En el anterior ejemplo de Hola, hay 24 segmentos de datos tal y como se produce cada segmento de datos cada hora.</span><span class="sxs-lookup"><span data-stu-id="9197f-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="9197f-218">Para obtener descripciones de las propiedades JSON en una definición de canalización, consulte cómo [crear canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9197f-219">Para obtener descripciones de las propiedades JSON en una definición de actividad de copia, consulte las [actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9197f-220">Para ver las descripciones de las propiedades JSON admitidas por BlobSource, consulte el artículo sobre el [conector de Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="9197f-221">Para ver las descripciones de las propiedades JSON admitidas por SqlSink, consulte el artículo sobre el [conector de Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="9197f-222">Definición de variables globales</span><span class="sxs-lookup"><span data-stu-id="9197f-222">Set global variables</span></span>
<span data-ttu-id="9197f-223">En Azure PowerShell, ejecute hello después de comandos después de reemplazar los valores de hello con su propio:</span><span class="sxs-lookup"><span data-stu-id="9197f-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9197f-224">Consulte la sección [Requisitos previos](#prerequisites) para obtener instrucciones sobre cómo obtener el identificador de cliente, el secreto del cliente, el identificador de inquilino y el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="9197f-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="9197f-225">Ejecute hello siguiente comando después de actualizar el nombre de Hola Hola factoría de datos que usa:</span><span class="sxs-lookup"><span data-stu-id="9197f-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="9197f-226">Autenticación con AAD</span><span class="sxs-lookup"><span data-stu-id="9197f-226">Authenticate with AAD</span></span>
<span data-ttu-id="9197f-227">Siguiente ejecución Hola comando tooauthenticate con Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="9197f-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="9197f-228">Creación de Data Factory</span><span class="sxs-lookup"><span data-stu-id="9197f-228">Create data factory</span></span>
<span data-ttu-id="9197f-229">En este paso, creará una instancia de Data Factory de Azure llamada **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="9197f-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="9197f-230">Una factoría de datos puede tener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="9197f-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="9197f-231">Una canalización puede tener una o más actividades.</span><span class="sxs-lookup"><span data-stu-id="9197f-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="9197f-232">Por ejemplo, una toocopy de datos de actividad de copia de un origen de datos de destino tooa almacenar.</span><span class="sxs-lookup"><span data-stu-id="9197f-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="9197f-233">Datos de salida de tooproduct de datos de entrada de un toorun de actividad de Hive de HDInsight un tootransform de script de Hive.</span><span class="sxs-lookup"><span data-stu-id="9197f-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="9197f-234">Ejecute hello después de la factoría de datos de comandos toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="9197f-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="9197f-235">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="9197f-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="9197f-236">Confirmar ese nombre Hola Hola factoría de datos que especifique aquí (ADFCopyTutorialDF) coincidencias Hola nombre especificado en hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="9197f-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9197f-237">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="9197f-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9197f-238">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-238">View hello results.</span></span> <span data-ttu-id="9197f-239">Si se ha creado correctamente la factoría de datos de hello, vea Hola JSON de factoría de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9197f-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="9197f-240">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="9197f-240">Note hello following points:</span></span>

* <span data-ttu-id="9197f-241">nombre de Hola de hello Data Factory de Azure debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="9197f-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="9197f-242">Si ve errores de hello en los resultados: **nombre de generador de datos "ADFCopyTutorialDF" no está disponible**, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9197f-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="9197f-243">Cambiar el nombre de hello (por ejemplo, yournameADFCopyTutorialDF) en hello **datafactory.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="9197f-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="9197f-244">En el primer comando de Hola Hola donde **$cmd** se asigna un valor variable, reemplace ADFCopyTutorialDF con el nombre nuevo de Hola y ejecute el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="9197f-245">Resultados de la ejecución toocreate de API de REST de hello dos comandos siguientes tooinvoke Hola Hola datos generador e impresión Hola de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="9197f-246">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="9197f-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="9197f-247">instancias de la factoría de datos de toocreate, deberá toobe un colaborador o administrador de hello suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="9197f-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="9197f-248">nombre Hola Hola factoría de datos se puede registrarse como un nombre DNS en hello futuras y, por tanto, están visible públicamente.</span><span class="sxs-lookup"><span data-stu-id="9197f-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="9197f-249">Si recibe el error hello: "**esta suscripción no tiene espacio de nombres registrado toouse Microsoft.DataFactory**", siga uno de los procedimientos de Hola e intente publicar de nuevo:</span><span class="sxs-lookup"><span data-stu-id="9197f-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="9197f-250">En Azure PowerShell, ejecute hello después de proveedor del comando tooregister Hola factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="9197f-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="9197f-251">Puede ejecutar Hola después comando tooconfirm ese Hola factoría de datos de proveedor está registrado.</span><span class="sxs-lookup"><span data-stu-id="9197f-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="9197f-252">Inicio de sesión mediante Hola suscripción de Azure en hello [portal de Azure](https://portal.azure.com) y navegar por hoja de la factoría de datos de tooa crear una factoría de datos en el portal de Azure hello (o).</span><span class="sxs-lookup"><span data-stu-id="9197f-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="9197f-253">Esta acción registra automáticamente proveedor Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="9197f-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="9197f-254">Antes de crear una canalización, necesita toocreate algunas entidades de la factoría de datos en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="9197f-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="9197f-255">En primer lugar crear origen de toolink servicios vinculados y tooyour datos de almacenes de datos de destino almacenar.</span><span class="sxs-lookup"><span data-stu-id="9197f-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="9197f-256">A continuación, defina los conjuntos de datos de entrada y salida toorepresent datos en almacenes de datos vinculado.</span><span class="sxs-lookup"><span data-stu-id="9197f-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="9197f-257">Finalmente, cree la canalización de Hola a una actividad que usa estos conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="9197f-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="9197f-258">Crear servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="9197f-258">Create linked services</span></span>
<span data-ttu-id="9197f-259">Crear servicios vinculados en un toolink de factoría de datos almacenan sus datos y se factoría de datos de toohello de servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="9197f-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="9197f-260">En este tutorial, no se usa ningún servicio de proceso, como Azure HDInsight o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9197f-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="9197f-261">Se usan dos almacenes de datos del tipo Azure Storage (origen) y Azure SQL Database (destino).</span><span class="sxs-lookup"><span data-stu-id="9197f-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="9197f-262">Por lo tanto, se crean dos servicios vinculados llamados AzureStorageLinkedService y AzureSqlLinkedService del tipo AzureStorage y AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="9197f-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="9197f-263">Hola AzureStorageLinkedService vincula su factoría de datos de toohello de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="9197f-264">Esta cuenta de almacenamiento es hello uno en el que se creó un contenedor y cargar datos de hello como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="9197f-265">AzureSqlLinkedService vincula su factoría de datos de toohello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="9197f-266">datos de Hola que se copian desde el almacenamiento de blobs de Hola se almacenan en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="9197f-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="9197f-267">Crear tabla emp de hello en esta base de datos como parte de [requisitos previos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9197f-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="9197f-268">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="9197f-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="9197f-269">En este paso, vincule la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="9197f-270">Especificar nombre de Hola y clave de la cuenta de almacenamiento de Azure en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9197f-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="9197f-271">Vea [servicio vinculado de almacenamiento de Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obtener más información sobre JSON toodefine de propiedades que se usan un almacenamiento de Azure servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="9197f-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="9197f-272">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="9197f-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9197f-273">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="9197f-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9197f-274">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-274">View hello results.</span></span> <span data-ttu-id="9197f-275">Si Hola vinculado se ha creado correctamente el servicio, vea Hola JSON para el servicio de hello vinculado en hello **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9197f-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="9197f-276">Creación de un servicio vinculado SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="9197f-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="9197f-277">En este paso, vincule la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="9197f-278">Especifique el nombre del servidor SQL Azure hello, nombre de base de datos, nombre de usuario y contraseña de usuario en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9197f-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="9197f-279">Vea [servicio vinculado de SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obtener más información acerca de toodefine de propiedades que se usan JSON SQL Azure servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="9197f-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="9197f-280">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="9197f-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9197f-281">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="9197f-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9197f-282">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-282">View hello results.</span></span> <span data-ttu-id="9197f-283">Si Hola vinculado se ha creado correctamente el servicio, vea Hola JSON para el servicio de hello vinculado en hello **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9197f-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="9197f-284">Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="9197f-284">Create datasets</span></span>
<span data-ttu-id="9197f-285">En el paso anterior de hello, crear servicios vinculados toolink su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="9197f-286">En este paso, definirá dos conjuntos de datos con el nombre AzureBlobInput y AzureSqlOutput que representan la entrada y los datos de salida que se almacenan en almacenes de datos de Hola que hace referencia AzureStorageLinkedService y AzureSqlLinkedService respectivamente.</span><span class="sxs-lookup"><span data-stu-id="9197f-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="9197f-287">servicio de almacenamiento de Azure vinculado de Hello especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en tiempo de ejecución tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="9197f-288">Y conjunto de datos de blob de entrada de hello (AzureBlobInput) especifica contenedor de Hola y la carpeta de Hola que contiene los datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="9197f-289">De forma similar, Hola servicio de base de datos de Azure SQL vinculado especifica cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="9197f-290">Y conjunto de datos de tabla SQL (OututDataset) especifica la tabla de Hola Hola Hola de toowhich de base de datos se copian datos desde almacenamiento de blobs de Hola de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="9197f-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="9197f-291">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="9197f-291">Create input dataset</span></span>
<span data-ttu-id="9197f-292">En este paso, creará un conjunto de datos denominado AzureBlobInput que apunta a un archivo blob tooa (emp.txt) en la carpeta raíz de Hola de un contenedor de blobs (adftutorial) en hello representado por hello AzureStorageLinkedService vinculado servicio de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="9197f-293">Si no especifica un valor para el nombre de archivo de hello (o puede omitirla), datos de todos los blobs en la carpeta de entrada de hello son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="9197f-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="9197f-294">En este tutorial, especifique un valor para el nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="9197f-295">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="9197f-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9197f-296">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="9197f-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9197f-297">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-297">View hello results.</span></span> <span data-ttu-id="9197f-298">Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9197f-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="9197f-299">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="9197f-299">Create output dataset</span></span>
<span data-ttu-id="9197f-300">Hola servicio de base de datos de Azure SQL vinculado especifica la cadena de conexión de Hola que usa el servicio de factoría de datos en la base de datos de tiempo de ejecución tooconnect tooyour SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="9197f-301">Hola salida SQL tabla conjunto de datos (OututDataset) se crea en este paso especifica se copia la tabla de hello en bases de datos Hola Hola toowhich Hola del almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9197f-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="9197f-302">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="9197f-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9197f-303">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="9197f-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9197f-304">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-304">View hello results.</span></span> <span data-ttu-id="9197f-305">Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9197f-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="9197f-306">Creación de una canalización</span><span class="sxs-lookup"><span data-stu-id="9197f-306">Create pipeline</span></span>
<span data-ttu-id="9197f-307">En este paso, creará una canalización con una **actividad de copia** que utiliza **AzureBlobInput** como entrada y **AzureSqlOutput** como salida.</span><span class="sxs-lookup"><span data-stu-id="9197f-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="9197f-308">Actualmente, el conjunto de datos de salida es qué unidades Hola programación.</span><span class="sxs-lookup"><span data-stu-id="9197f-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="9197f-309">En este tutorial, el conjunto de datos de salida es tooproduce configurado un segmento una vez cada hora.</span><span class="sxs-lookup"><span data-stu-id="9197f-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="9197f-310">canalización de Hello tiene una hora de inicio y la hora de finalización que son un día separado, lo que es de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="9197f-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="9197f-311">Por lo tanto, 24 segmentos del conjunto de datos de salida generados por la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="9197f-312">Asignar Hola comando toovariable denominado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="9197f-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9197f-313">Ejecutar comandos de hello mediante **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="9197f-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9197f-314">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-314">View hello results.</span></span> <span data-ttu-id="9197f-315">Si se ha creado correctamente el conjunto de datos de hello, vea hello JSON para el conjunto de datos de Hola Hola **resultados**; en caso contrario, verá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9197f-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="9197f-316">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="9197f-316">**Congratulations!**</span></span> <span data-ttu-id="9197f-317">Ha creado correctamente una factoría de datos de Azure, con una canalización que copia datos de base de datos SQL de tooAzure de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="9197f-318">Supervisión de la canalización</span><span class="sxs-lookup"><span data-stu-id="9197f-318">Monitor pipeline</span></span>
<span data-ttu-id="9197f-319">En este paso, utilice sectores de toomonitor de API de REST de factoría de datos se está generados en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="9197f-320">Asegúrese de que Hola inicial y final horas después de hello especificado en comando coincidencia Hola inicio y finalización de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="9197f-321">Ejecute Invoke-Command Hola y Hola siguiente hasta que vea un segmento en **listo** estado o **error** estado.</span><span class="sxs-lookup"><span data-stu-id="9197f-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="9197f-322">Al segmento de hello está en estado listo, comprobar hello **emp** tabla en la base de datos de SQL Azure para datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="9197f-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="9197f-323">Para cada sector, dos filas de datos de archivo de código fuente de hello son tabla emp de toohello copiados en la base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="9197f-324">Por lo tanto, verá 24 nuevos registros en la tabla emp de hello cuando se han procesado correctamente todos los sectores de hello (en estado listo).</span><span class="sxs-lookup"><span data-stu-id="9197f-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="9197f-325">Resumen</span><span class="sxs-lookup"><span data-stu-id="9197f-325">Summary</span></span>
<span data-ttu-id="9197f-326">En este tutorial, ha utilizado la API de REST toocreate un Azure generador toocopy datos desde una base de datos de SQL Azure de tooan de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="9197f-327">Estos son los pasos de alto nivel de hello realizadas en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="9197f-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="9197f-328">Ha creado una **factoría de datos**de Azure.</span><span class="sxs-lookup"><span data-stu-id="9197f-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="9197f-329">Ha creado **servicios vinculados**.</span><span class="sxs-lookup"><span data-stu-id="9197f-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="9197f-330">Un almacenamiento de Azure había vinculada servicio toolink su cuenta de almacenamiento de Azure que contiene datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="9197f-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="9197f-331">SQL Azure había vinculado toolink servicio base de datos SQL de Azure que contiene los datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="9197f-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="9197f-332">Ha creado **conjuntos de datos**que describen los datos de entrada y salida para las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="9197f-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="9197f-333">Ha creado una **canalización** con una actividad de copia con un origen BlobSource y un receptor SqlSink.</span><span class="sxs-lookup"><span data-stu-id="9197f-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9197f-334">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9197f-334">Next steps</span></span>
<span data-ttu-id="9197f-335">En este tutorial, ha usado Azure Blob Storage como almacén de datos de origen y una base de datos SQL de Azure como almacén de datos de destino en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="9197f-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="9197f-336">Hello tabla siguiente proporciona una lista de almacenes de datos que se admiten como orígenes y destinos por actividad de copia de hello:</span><span class="sxs-lookup"><span data-stu-id="9197f-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="9197f-337">toolearn acerca de cómo almacenan datos toocopy de datos, haga clic en vínculo Hola Hola de almacén de datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9197f-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
