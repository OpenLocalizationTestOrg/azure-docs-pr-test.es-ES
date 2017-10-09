---
title: "aaaCreate características de Azure blob de datos de almacenamiento mediante Panda | Documentos de Microsoft"
description: "Cómo toocreate características para los datos que se almacenan en el contenedor de blobs de Azure con el paquete de Python Panda Hola."
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
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="eb553-103">Creación de características para los datos de almacenamiento de blobs de Azure mediante Panda</span><span class="sxs-lookup"><span data-stu-id="eb553-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="eb553-104">Este documento muestra cómo las características de los datos que se almacenan en el contenedor de blobs de Azure mediante hello toocreate [Pandas](http://pandas.pydata.org/) paquete de Python.</span><span class="sxs-lookup"><span data-stu-id="eb553-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="eb553-105">Después de esquematizar cómo datos de hello tooload dentro de una trama de datos de Panda, muestra cómo toogenerate las características de categorías mediante scripts de Python con valores de indicador y características de discretización.</span><span class="sxs-lookup"><span data-stu-id="eb553-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="eb553-106">Esto **menú** vincula tootopics que describen cómo toocreate características para los datos en varios entornos.</span><span class="sxs-lookup"><span data-stu-id="eb553-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="eb553-107">Esta tarea es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="eb553-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb553-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eb553-108">Prerequisites</span></span>
<span data-ttu-id="eb553-109">En este artículo se supone que ja creado una cuenta de almacenamiento de blobs de Azure y que ha almacenado los datos ahí.</span><span class="sxs-lookup"><span data-stu-id="eb553-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="eb553-110">Si necesita instrucciones tooset una cuenta, consulte [crear una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="eb553-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="eb553-111">Cargar datos de hello en una trama de datos Pandas</span><span class="sxs-lookup"><span data-stu-id="eb553-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="eb553-112">En orden toodo explorar y manipular un conjunto de datos, debe descargarse de hello blob origen tooa archivo local que, a continuación, se pueden cargar en una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="eb553-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="eb553-113">A continuación, incluimos hello toofollow de pasos para realizar este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="eb553-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="eb553-114">Descargar datos Hola de Azure blob con hello después el código Python de ejemplo con servicio de blobs.</span><span class="sxs-lookup"><span data-stu-id="eb553-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="eb553-115">Reemplace la variable de hello en el código de hello a continuación con los valores específicos:</span><span class="sxs-lookup"><span data-stu-id="eb553-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="eb553-116">Leer datos de hello en una trama de datos Pandas de hello descargan el archivo.</span><span class="sxs-lookup"><span data-stu-id="eb553-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="eb553-117">Ahora va a datos de hello tooexplore listo y genera características en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="eb553-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="eb553-118"><a name="blob-featuregen"></a>Generación de características</span><span class="sxs-lookup"><span data-stu-id="eb553-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="eb553-119">Hola dos secciones siguientes mostrar cómo toogenerate las características de categorías con valores de indicador y discretización características mediante scripts de Python.</span><span class="sxs-lookup"><span data-stu-id="eb553-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="eb553-120"><a name="blob-countfeature"></a>Generación de características basada en el valor de indicador</span><span class="sxs-lookup"><span data-stu-id="eb553-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="eb553-121">Las características de categorías se pueden crear como sigue:</span><span class="sxs-lookup"><span data-stu-id="eb553-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="eb553-122">Inspeccionar la distribución de Hola de columna de categorías de hello:</span><span class="sxs-lookup"><span data-stu-id="eb553-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="eb553-123">Generar valores de indicador para cada uno de los valores de columna de Hola</span><span class="sxs-lookup"><span data-stu-id="eb553-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="eb553-124">Unirse a la columna de indicador de hello con trama de datos original de Hola</span><span class="sxs-lookup"><span data-stu-id="eb553-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="eb553-125">Quitar la propia variable original de hello:</span><span class="sxs-lookup"><span data-stu-id="eb553-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="eb553-126"><a name="blob-binningfeature"></a>Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="eb553-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="eb553-127">Para generar características discretizadas, se procede de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="eb553-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="eb553-128">Agregar una secuencia de columnas toobin una columna numérica</span><span class="sxs-lookup"><span data-stu-id="eb553-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="eb553-129">Convierte la secuencia de tooa discretización de las variables booleanas</span><span class="sxs-lookup"><span data-stu-id="eb553-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="eb553-130">Por último, las variables ficticias de Hola de combinación nuevamente toohello trama de datos original</span><span class="sxs-lookup"><span data-stu-id="eb553-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="eb553-131"><a name="sql-featuregen"></a>Hacer copia de escribir datos blob tooAzure y consume en aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="eb553-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="eb553-132">Una vez haya explorar datos hello y crea Hola características necesarias, puede cargar datos de hello (muestrear o caracterizará) tooan Azure blob y usarla en aprendizaje automático de Azure con hello pasos: tenga en cuenta que las características adicionales se pueden crear en hello Azure estudio de aprendizaje automático también.</span><span class="sxs-lookup"><span data-stu-id="eb553-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="eb553-133">Escribir en el archivo de hello datos marco toolocal</span><span class="sxs-lookup"><span data-stu-id="eb553-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="eb553-134">Cargar blob de hello datos tooAzure como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="eb553-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="eb553-135">Ahora puede leer datos de Hola de hello blob mediante Hola aprendizaje automático de Azure [importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) módulo tal y como se muestra en la pantalla de bienvenida a continuación:</span><span class="sxs-lookup"><span data-stu-id="eb553-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![lector de blobs](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

