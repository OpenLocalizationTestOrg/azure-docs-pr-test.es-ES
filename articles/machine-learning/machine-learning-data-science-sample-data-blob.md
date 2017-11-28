---
title: almacenamiento de blobs de datos aaaSample en Azure | Documentos de Microsoft
description: Muestra de datos en el almacenamiento de blobs de Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="b92da-103"><a name="heading"></a>Muestra de datos en el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="b92da-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="b92da-104">En este documento se tratan los datos de muestreo almacenados en el almacenamiento de blobs de Azure descargándolos mediante programación y luego realizando un muestreo de los mismos con procedimientos escritos en Python.</span><span class="sxs-lookup"><span data-stu-id="b92da-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="b92da-105">siguiente Hello **menú** vincula tootopics que describen cómo toosample datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b92da-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="b92da-106">**¿Por qué realizar un muestreo de los datos?**</span><span class="sxs-lookup"><span data-stu-id="b92da-106">**Why sample your data?**</span></span>
<span data-ttu-id="b92da-107">Si piensa tooanalyze de conjunto de datos de hello es grande, normalmente es un tooreduce de datos de ejemplo toodown Hola buena idea tooa más pequeño pero representativo y más fáciles de administrar el tamaño.</span><span class="sxs-lookup"><span data-stu-id="b92da-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="b92da-108">Esto facilita la comprensión y exploración de los datos, y el diseño de características.</span><span class="sxs-lookup"><span data-stu-id="b92da-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="b92da-109">Su función en el proceso de análisis de Cortana de hello es tooenable la creación de prototipos rápida de las funciones de procesamiento de datos de Hola y modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="b92da-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="b92da-110">Esta tarea de muestreo es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="b92da-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="b92da-111">Descarga y muestreado de datos</span><span class="sxs-lookup"><span data-stu-id="b92da-111">Download and down-sample data</span></span>
1. <span data-ttu-id="b92da-112">Descargar datos Hola desde el almacenamiento de blobs de Azure mediante servicio de blobs de Hola de hello después el código Python de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b92da-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="b92da-113">Leer datos en una trama de datos Pandas de archivo hello descargado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b92da-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="b92da-114">Datos de hello mediante Hola de ejemplo de abajo `numpy`del `random.choice` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b92da-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="b92da-115">Ahora puede trabajar con hello por encima de la trama de datos de ejemplo de Hola 1 por ciento de exploración más a fondo y la generación de la característica.</span><span class="sxs-lookup"><span data-stu-id="b92da-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="b92da-116"><a name="heading"></a>Carga de datos y lectura en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b92da-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="b92da-117">Puede usar después de datos de ejemplo toodown Hola de código de ejemplo de Hola y usarlo directamente en aprendizaje automático de Azure:</span><span class="sxs-lookup"><span data-stu-id="b92da-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="b92da-118">Escribir en el archivo local de hello datos marco tooa</span><span class="sxs-lookup"><span data-stu-id="b92da-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="b92da-119">Cargar archivo local de hello tooan Azure blob mediante el siguiente código de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b92da-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. <span data-ttu-id="b92da-120">Leer datos de Hola de hello Azure blob mediante aprendizaje automático de Azure [importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) tal y como se muestra en la imagen de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="b92da-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![lector de blobs](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

