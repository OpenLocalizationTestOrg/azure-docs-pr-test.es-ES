---
title: "Creación de características para los datos de Azure Blob Storage mediante Panda | Microsoft Docs"
description: "Cómo crear características para los datos almacenados en un contenedor de blobs de Azure mediante el paquete Panda de Python."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="c116a-103">Creación de características para los datos de almacenamiento de blobs de Azure mediante Panda</span><span class="sxs-lookup"><span data-stu-id="c116a-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="c116a-104">Este documento muestra cómo crear características para datos que se almacenan en el contenedor de blobs de Azure mediante el paquete de Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="c116a-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="c116a-105">Después de esquematizar cómo cargar los datos en una trama de datos de Panda, se muestra cómo generar características de categorías mediante scripts de Python con valores de indicador y características de discretización, mediante scripts de Python.</span><span class="sxs-lookup"><span data-stu-id="c116a-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="c116a-106">Este **menú** vincula a temas en los que se describe cómo crear características para datos en diversos entornos.</span><span class="sxs-lookup"><span data-stu-id="c116a-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="c116a-107">Esta tarea constituye un paso del [proceso de ciencia de datos en equipos (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="c116a-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c116a-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c116a-108">Prerequisites</span></span>
<span data-ttu-id="c116a-109">En este artículo se supone que ja creado una cuenta de almacenamiento de blobs de Azure y que ha almacenado los datos ahí.</span><span class="sxs-lookup"><span data-stu-id="c116a-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="c116a-110">Si necesita instrucciones para configurar una cuenta, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="c116a-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="c116a-111">Carga de los datos en una trama de datos Pandas</span><span class="sxs-lookup"><span data-stu-id="c116a-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="c116a-112">Para explorar y manipular un conjunto de datos, se debe descargar desde el origen de blob en un archivo local que se pueda cargar en una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="c116a-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="c116a-113">Estos son los pasos a seguir para realizar este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="c116a-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="c116a-114">Descargue los datos del blob de Azure con el siguiente código de Python de ejemplo mediante el servicio BLOB.</span><span class="sxs-lookup"><span data-stu-id="c116a-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="c116a-115">Reemplace la variable en el código siguiente por sus valores específicos:</span><span class="sxs-lookup"><span data-stu-id="c116a-115">Replace the variable in the code below with your specific values:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="c116a-116">Lea los datos en una trama de datos de Pandas desde el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="c116a-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="c116a-117">Ya puede explorar los datos y generar características en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="c116a-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="c116a-118"><a name="blob-featuregen"></a>Generación de características</span><span class="sxs-lookup"><span data-stu-id="c116a-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="c116a-119">Las dos secciones siguientes muestran cómo generar características de categorías con valores de indicador y características de discretización mediante scripts de Python.</span><span class="sxs-lookup"><span data-stu-id="c116a-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="c116a-120"><a name="blob-countfeature"></a>Generación de características basada en el valor de indicador</span><span class="sxs-lookup"><span data-stu-id="c116a-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="c116a-121">Las características de categorías se pueden crear como sigue:</span><span class="sxs-lookup"><span data-stu-id="c116a-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="c116a-122">Inspeccione la distribución de la columna de categorías:</span><span class="sxs-lookup"><span data-stu-id="c116a-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="c116a-123">Genere valores de indicador para cada uno de los valores de columna</span><span class="sxs-lookup"><span data-stu-id="c116a-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="c116a-124">Combine la columna de indicador con la trama de datos original</span><span class="sxs-lookup"><span data-stu-id="c116a-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="c116a-125">Quite la propia variable original:</span><span class="sxs-lookup"><span data-stu-id="c116a-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="c116a-126"><a name="blob-binningfeature"></a>Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="c116a-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="c116a-127">Para generar características discretizadas, se procede de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c116a-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="c116a-128">Agregue una secuencia de columnas para discretizar una columna numérica</span><span class="sxs-lookup"><span data-stu-id="c116a-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="c116a-129">Convierta la discretización en una secuencia de variables booleanas</span><span class="sxs-lookup"><span data-stu-id="c116a-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="c116a-130">Por último, combine las variables de prueba con la trama de datos original</span><span class="sxs-lookup"><span data-stu-id="c116a-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="c116a-131"><a name="sql-featuregen"></a>Reescritura de datos en un blob de Azure y consumo en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="c116a-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="c116a-132">Cuando haya explorado los datos y creado las características necesarias, puede cargar los datos (muestreados o con características) en un blob de Azure y consumirlos en Aprendizaje automático de Azure, mediante los siguientes pasos. Tenga en cuenta que también se pueden crear características adicionales en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="c116a-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="c116a-133">Escriba la trama de datos en el archivo local</span><span class="sxs-lookup"><span data-stu-id="c116a-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="c116a-134">Cargue los datos en el blob de Azure como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c116a-134">Upload the data to Azure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="c116a-135">Ahora se pueden leer los datos del blob mediante el módulo [Importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) de Aprendizaje automático de Azure, como se muestra en la pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="c116a-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![lector de blobs](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

