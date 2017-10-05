---
title: "Exploración de datos en Azure Blob Storage con Pandas | Microsoft Docs"
description: "Cómo explorar los datos almacenados en el contenedor de blobs de Azure mediante Pandas."
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
ms.openlocfilehash: e1b33b17270122a38228484a56c8324c5b4505a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="b93ad-103">Exploración de datos en el almacenamiento de blobs de Azure con Pandas</span><span class="sxs-lookup"><span data-stu-id="b93ad-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="b93ad-104">Este documento explica cómo explorar los datos almacenados en el contenedor de blobs de Azure mediante el paquete de Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="b93ad-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="b93ad-105">El siguiente **menú** vincula a temas que describen cómo usar herramientas para explorar los datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b93ad-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="b93ad-106">Esta tarea constituye un paso del [proceso de ciencia de datos en equipos (TDSP)]().</span><span class="sxs-lookup"><span data-stu-id="b93ad-106">This task is a step in the [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="b93ad-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b93ad-107">Prerequisites</span></span>
<span data-ttu-id="b93ad-108">En este artículo se supone que ha:</span><span class="sxs-lookup"><span data-stu-id="b93ad-108">This article assumes that you have:</span></span>

* <span data-ttu-id="b93ad-109">Creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b93ad-109">Created an Azure storage account.</span></span> <span data-ttu-id="b93ad-110">Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b93ad-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="b93ad-111">Almacenó los datos en una cuenta de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="b93ad-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="b93ad-112">Si necesita instrucciones, consulte [mover con Azure Storage como origen y destino](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="b93ad-112">If you need instructions, see [Moving data to and from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="b93ad-113">Carga de los datos en una trama de datos de Pandas</span><span class="sxs-lookup"><span data-stu-id="b93ad-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="b93ad-114">Para explorar y manipular un conjunto de datos, se debe descargar desde el origen de blob en un archivo local que se pueda cargar en una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="b93ad-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="b93ad-115">Estos son los pasos a seguir para realizar este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="b93ad-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="b93ad-116">Descargue los datos del blob de Azure con el siguiente código de ejemplo Python mediante el servicio BLOB.</span><span class="sxs-lookup"><span data-stu-id="b93ad-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="b93ad-117">Reemplace la variable en el código siguiente por sus valores específicos:</span><span class="sxs-lookup"><span data-stu-id="b93ad-117">Replace the variable in the following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="b93ad-118">Lea los datos en una trama de datos de Pandas desde el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="b93ad-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="b93ad-119">Ya puede explorar los datos y generar características en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="b93ad-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="b93ad-120"><a name="blob-dataexploration"></a>Ejemplos de exploración de datos con Pandas</span><span class="sxs-lookup"><span data-stu-id="b93ad-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="b93ad-121">A continuación, se muestran algunos ejemplos de formas de explorar datos mediante Pandas:</span><span class="sxs-lookup"><span data-stu-id="b93ad-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="b93ad-122">Inspeccionar el **número de filas y columnas**</span><span class="sxs-lookup"><span data-stu-id="b93ad-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="b93ad-123">**Inspeccionar** las primeras o las últimas **filas** del conjunto de datos, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b93ad-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="b93ad-124">Comprobar el **tipo de datos** como el que se importó cada columna mediante el siguiente código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b93ad-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="b93ad-125">Comprobar las **estadísticas básicas** de las columnas del conjunto de datos de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="b93ad-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="b93ad-126">Observar el número de entradas de cada valor de columna, como se indica a continuación</span><span class="sxs-lookup"><span data-stu-id="b93ad-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="b93ad-127">**Contar los valores que faltan** frente al número real de entradas de cada columna, mediante el siguiente código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b93ad-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="b93ad-128">Si hay **valores que faltan** para una columna determinada en los datos, puede quitarlos como se indica:</span><span class="sxs-lookup"><span data-stu-id="b93ad-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="b93ad-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="b93ad-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="b93ad-130">Otra forma de reemplazar los valores que faltan es a través de la función de modo:</span><span class="sxs-lookup"><span data-stu-id="b93ad-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="b93ad-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="b93ad-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="b93ad-132">Crear un gráfico de **histograma** con un número variable de discretizaciones para trazar la distribución de una variable.</span><span class="sxs-lookup"><span data-stu-id="b93ad-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="b93ad-133">Examinar las **correlaciones** entre las variables mediante un gráfico de dispersión o con la función de correlación integrada.</span><span class="sxs-lookup"><span data-stu-id="b93ad-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

