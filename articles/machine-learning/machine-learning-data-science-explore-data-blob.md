---
title: aaaExplore datos en Azure blob storage con Pandas | Documentos de Microsoft
description: "¿Cómo tooexplore datos que se almacenan en Azure blob contenedor mediante Pandas."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="cf09a-103">Exploración de datos en el almacenamiento de blobs de Azure con Pandas</span><span class="sxs-lookup"><span data-stu-id="cf09a-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="cf09a-104">Este documento cubre cómo tooexplore datos que se almacenan en Azure blob contenedor mediante [Pandas](http://pandas.pydata.org/) paquete de Python.</span><span class="sxs-lookup"><span data-stu-id="cf09a-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="cf09a-105">siguiente Hello **menú** vincula tootopics que describen cómo toouse herramientas tooexplore datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cf09a-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="cf09a-106">Esta tarea es un paso en hello [proceso de ciencia de datos]().</span><span class="sxs-lookup"><span data-stu-id="cf09a-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="cf09a-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cf09a-107">Prerequisites</span></span>
<span data-ttu-id="cf09a-108">En este artículo se supone que ha:</span><span class="sxs-lookup"><span data-stu-id="cf09a-108">This article assumes that you have:</span></span>

* <span data-ttu-id="cf09a-109">Creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf09a-109">Created an Azure storage account.</span></span> <span data-ttu-id="cf09a-110">Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="cf09a-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="cf09a-111">Almacenó los datos en una cuenta de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf09a-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="cf09a-112">Si necesita instrucciones, consulte [tooand de mover datos desde el almacenamiento de Azure](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="cf09a-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="cf09a-113">Cargar datos de hello en una trama de datos de Pandas</span><span class="sxs-lookup"><span data-stu-id="cf09a-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="cf09a-114">tooexplore y manipular un conjunto de datos, primero debe descargarse de hello blob origen tooa archivo local, que, a continuación, se pueden cargar en una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="cf09a-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="cf09a-115">A continuación, incluimos hello toofollow de pasos para realizar este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="cf09a-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="cf09a-116">Descargar datos Hola de Azure blob con hello siguiendo el ejemplo de código de Python mediante servicio de blobs.</span><span class="sxs-lookup"><span data-stu-id="cf09a-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="cf09a-117">Reemplace la variable de Hola Hola después el código con los valores específicos:</span><span class="sxs-lookup"><span data-stu-id="cf09a-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="cf09a-118">Leer datos de hello en una trama de datos Pandas de hello descargan el archivo.</span><span class="sxs-lookup"><span data-stu-id="cf09a-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="cf09a-119">Ahora va a datos de hello tooexplore listo y genera características en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="cf09a-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="cf09a-120"><a name="blob-dataexploration"></a>Ejemplos de exploración de datos con Pandas</span><span class="sxs-lookup"><span data-stu-id="cf09a-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="cf09a-121">Estos son algunos ejemplos de formas de datos de tooexplore mediante Pandas:</span><span class="sxs-lookup"><span data-stu-id="cf09a-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="cf09a-122">Inspeccionar hello **número de filas y columnas**</span><span class="sxs-lookup"><span data-stu-id="cf09a-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="cf09a-123">**Inspeccionar** Hola algunos primeros o últimos **filas** Hola siguiendo el conjunto de datos:</span><span class="sxs-lookup"><span data-stu-id="cf09a-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="cf09a-124">Comprobar hello **tipo de datos** cada columna se importó como mediante el siguiente código de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="cf09a-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="cf09a-125">Comprobar hello **estadísticas básicas** para columnas Hola de Hola conjunto de datos como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="cf09a-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="cf09a-126">Busque Hola número de entradas para cada valor de columna como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="cf09a-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="cf09a-127">**Recuento de valores que faltan** frente a un número real de entradas de cada columna mediante el siguiente código de ejemplo de Hola Hola</span><span class="sxs-lookup"><span data-stu-id="cf09a-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="cf09a-128">Si tiene **valores que faltan** para una columna concreta de datos de hello, puede arrastrar como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="cf09a-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="cf09a-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="cf09a-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="cf09a-130">Valores que faltan de otra manera tooreplace es con la función de modo de hello:</span><span class="sxs-lookup"><span data-stu-id="cf09a-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="cf09a-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="cf09a-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="cf09a-132">Crear un **histograma** trazado mediante un número variable de distribución de hello tooplot de cubos de una variable</span><span class="sxs-lookup"><span data-stu-id="cf09a-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="cf09a-133">Mire **correlaciones** entre las variables utilizando un scatterplot u Hola integrados correlation, función</span><span class="sxs-lookup"><span data-stu-id="cf09a-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

