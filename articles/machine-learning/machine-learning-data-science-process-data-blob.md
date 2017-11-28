---
title: "datos con análisis avanzado de blobs de Azure aaaProcess | Documentos de Microsoft"
description: Proceso de datos en Almacenamiento de blobs de Azure.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="09769-103"><a name="heading"></a>Proceso de datos del blob de Azure con análisis avanzado</span><span class="sxs-lookup"><span data-stu-id="09769-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="09769-104">En este documento se trata la exploración de datos y generación de características a partir de los datos almacenados en Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="09769-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="09769-105">Cargar datos de hello en una trama de datos Pandas</span><span class="sxs-lookup"><span data-stu-id="09769-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="09769-106">En orden tooexplore y manipular un conjunto de datos, debe descargarse de hello blob origen tooa archivo local que, a continuación, se pueden cargar en una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="09769-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="09769-107">A continuación, incluimos hello toofollow de pasos para realizar este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="09769-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="09769-108">Descargar datos Hola de Azure blob con hello después el código Python de ejemplo con servicio de blobs.</span><span class="sxs-lookup"><span data-stu-id="09769-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="09769-109">Reemplace la variable de hello en el código de hello a continuación con los valores específicos:</span><span class="sxs-lookup"><span data-stu-id="09769-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="09769-110">Leer datos de hello en una trama de datos Pandas de hello descargan el archivo.</span><span class="sxs-lookup"><span data-stu-id="09769-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="09769-111">Ahora va a datos de hello tooexplore listo y genera características en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="09769-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="09769-112"><a name="blob-dataexploration"></a>Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="09769-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="09769-113">Estos son algunos ejemplos de formas de datos de tooexplore mediante Pandas:</span><span class="sxs-lookup"><span data-stu-id="09769-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="09769-114">Inspeccionar Hola número de filas y columnas</span><span class="sxs-lookup"><span data-stu-id="09769-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="09769-115">Inspeccionar Hola primero o último algunas filas de conjunto de datos de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="09769-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="09769-116">Comprobar tipo de datos de hello que cada columna se importó como mediante el siguiente código de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="09769-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="09769-117">Comprobar estadísticas básicas de Hola para las columnas de Hola Hola conjunto de datos como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="09769-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="09769-118">Busque Hola número de entradas para cada valor de columna como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="09769-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="09769-119">Recuento de valores que faltan frente a un número real de entradas de cada columna mediante el siguiente código de ejemplo de Hola Hola</span><span class="sxs-lookup"><span data-stu-id="09769-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="09769-120">Si tiene los valores que faltan para una columna específica en los datos de hello, puede colocarlas como sigue:</span><span class="sxs-lookup"><span data-stu-id="09769-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="09769-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="09769-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="09769-122">Valores que faltan de otra manera tooreplace es con la función de modo de hello:</span><span class="sxs-lookup"><span data-stu-id="09769-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="09769-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="09769-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="09769-124">Crear un gráfico de histograma con un número variable de distribución de hello tooplot de cubos de una variable</span><span class="sxs-lookup"><span data-stu-id="09769-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="09769-125">Examine las correlaciones entre las variables utilizando un scatterplot u Hola integrados correlation, función</span><span class="sxs-lookup"><span data-stu-id="09769-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="09769-126"><a name="blob-featuregen"></a>Generación de características</span><span class="sxs-lookup"><span data-stu-id="09769-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="09769-127">Es posible generar características con Python de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="09769-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="09769-128"><a name="blob-countfeature"></a>Generación de características basada en el valor de indicador</span><span class="sxs-lookup"><span data-stu-id="09769-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="09769-129">Las características de categorías se pueden crear como sigue:</span><span class="sxs-lookup"><span data-stu-id="09769-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="09769-130">Inspeccionar la distribución de Hola de columna de categorías de hello:</span><span class="sxs-lookup"><span data-stu-id="09769-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="09769-131">Generar valores de indicador para cada uno de los valores de columna de Hola</span><span class="sxs-lookup"><span data-stu-id="09769-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="09769-132">Unirse a la columna de indicador de hello con trama de datos original de Hola</span><span class="sxs-lookup"><span data-stu-id="09769-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="09769-133">Quitar la propia variable original de hello:</span><span class="sxs-lookup"><span data-stu-id="09769-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="09769-134"><a name="blob-binningfeature"></a>Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="09769-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="09769-135">Para generar características discretizadas, se procede de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="09769-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="09769-136">Agregar una secuencia de columnas toobin una columna numérica</span><span class="sxs-lookup"><span data-stu-id="09769-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="09769-137">Convierte la secuencia de tooa discretización de las variables booleanas</span><span class="sxs-lookup"><span data-stu-id="09769-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="09769-138">Por último, las variables ficticias de Hola de combinación nuevamente toohello trama de datos original</span><span class="sxs-lookup"><span data-stu-id="09769-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="09769-139"><a name="sql-featuregen"></a>Hacer copia de escribir datos blob tooAzure y consume en aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="09769-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="09769-140">Una vez haya explorar datos hello y crea Hola características necesarias, puede cargar datos de hello (muestrear o caracterizará) tooan Azure blob y usarla en aprendizaje automático de Azure con hello pasos: tenga en cuenta que las características adicionales se pueden crear en hello Azure estudio de aprendizaje automático también.</span><span class="sxs-lookup"><span data-stu-id="09769-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="09769-141">Escribir en el archivo de hello datos marco toolocal</span><span class="sxs-lookup"><span data-stu-id="09769-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="09769-142">Cargar blob de hello datos tooAzure como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="09769-142">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="09769-143">Ahora puede leer datos de Hola de hello blob mediante Hola aprendizaje automático de Azure [importar datos] [ import-data] módulo tal y como se muestra en la pantalla de bienvenida a continuación:</span><span class="sxs-lookup"><span data-stu-id="09769-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![lector de blobs][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

