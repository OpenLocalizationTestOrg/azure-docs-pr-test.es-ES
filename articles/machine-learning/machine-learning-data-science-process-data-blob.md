---
title: "Proceso de datos del blob de Azure con análisis avanzado | Microsoft Docs"
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="b7b45-103"><a name="heading"></a>Proceso de datos del blob de Azure con análisis avanzado</span><span class="sxs-lookup"><span data-stu-id="b7b45-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="b7b45-104">En este documento se trata la exploración de datos y generación de características a partir de los datos almacenados en Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7b45-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="b7b45-105">Carga de los datos en una trama de datos Pandas</span><span class="sxs-lookup"><span data-stu-id="b7b45-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="b7b45-106">Para explorar y manipular un conjunto de datos, se debe descargar desde el origen de blob en un archivo local que se pueda cargar en una trama de datos de Pandas.</span><span class="sxs-lookup"><span data-stu-id="b7b45-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="b7b45-107">Estos son los pasos a seguir para realizar este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="b7b45-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="b7b45-108">Descargue los datos del blob de Azure con el siguiente código de Python de ejemplo mediante el servicio BLOB.</span><span class="sxs-lookup"><span data-stu-id="b7b45-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="b7b45-109">Reemplace la variable en el código siguiente por sus valores específicos:</span><span class="sxs-lookup"><span data-stu-id="b7b45-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="b7b45-110">Lea los datos en una trama de datos de Pandas desde el archivo descargado.</span><span class="sxs-lookup"><span data-stu-id="b7b45-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="b7b45-111">Ya puede explorar los datos y generar características en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="b7b45-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="b7b45-112"><a name="blob-dataexploration"></a>Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="b7b45-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="b7b45-113">A continuación, se muestran algunos ejemplos de formas de explorar datos mediante Pandas:</span><span class="sxs-lookup"><span data-stu-id="b7b45-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="b7b45-114">Inspeccionar el número de filas y columnas</span><span class="sxs-lookup"><span data-stu-id="b7b45-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="b7b45-115">Inspeccionar las primeras o las últimas filas del conjunto de datos, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b7b45-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="b7b45-116">Comprobar el tipo de datos como el que se importó cada columna mediante el siguiente código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b7b45-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="b7b45-117">Comprobar las estadísticas básicas de las columnas del conjunto de datos de la siguiente forma</span><span class="sxs-lookup"><span data-stu-id="b7b45-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="b7b45-118">Observar el número de entradas de cada valor de columna, como se indica a continuación</span><span class="sxs-lookup"><span data-stu-id="b7b45-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="b7b45-119">Contar los valores que faltan frente al número real de entradas de cada columna, mediante el siguiente código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b7b45-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="b7b45-120">Si hay valores que faltan para una columna determinada en los datos, puede quitarlos como se indica:</span><span class="sxs-lookup"><span data-stu-id="b7b45-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="b7b45-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="b7b45-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="b7b45-122">Otra forma de reemplazar los valores que faltan es a través de la función de modo:</span><span class="sxs-lookup"><span data-stu-id="b7b45-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="b7b45-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="b7b45-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="b7b45-124">Crear un gráfico de histograma con un número variable de discretizaciones para trazar la distribución de una variable</span><span class="sxs-lookup"><span data-stu-id="b7b45-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="b7b45-125">Examinar las correlaciones entre las variables mediante un gráfico de dispersión o con la función de correlación integrada</span><span class="sxs-lookup"><span data-stu-id="b7b45-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="b7b45-126"><a name="blob-featuregen"></a>Generación de características</span><span class="sxs-lookup"><span data-stu-id="b7b45-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="b7b45-127">Es posible generar características con Python de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="b7b45-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="b7b45-128"><a name="blob-countfeature"></a>Generación de características basada en el valor de indicador</span><span class="sxs-lookup"><span data-stu-id="b7b45-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="b7b45-129">Las características de categorías se pueden crear como sigue:</span><span class="sxs-lookup"><span data-stu-id="b7b45-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="b7b45-130">Inspeccione la distribución de la columna de categorías:</span><span class="sxs-lookup"><span data-stu-id="b7b45-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="b7b45-131">Genere valores de indicador para cada uno de los valores de columna</span><span class="sxs-lookup"><span data-stu-id="b7b45-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="b7b45-132">Combine la columna de indicador con la trama de datos original</span><span class="sxs-lookup"><span data-stu-id="b7b45-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="b7b45-133">Quite la propia variable original:</span><span class="sxs-lookup"><span data-stu-id="b7b45-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="b7b45-134"><a name="blob-binningfeature"></a>Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="b7b45-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="b7b45-135">Para generar características discretizadas, se procede de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="b7b45-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="b7b45-136">Agregue una secuencia de columnas para discretizar una columna numérica</span><span class="sxs-lookup"><span data-stu-id="b7b45-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="b7b45-137">Convierta la discretización en una secuencia de variables booleanas</span><span class="sxs-lookup"><span data-stu-id="b7b45-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="b7b45-138">Por último, combine las variables de prueba con la trama de datos original</span><span class="sxs-lookup"><span data-stu-id="b7b45-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="b7b45-139"><a name="sql-featuregen"></a>Reescritura de datos en un blob de Azure y consumo en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b7b45-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="b7b45-140">Cuando haya explorado los datos y creado las características necesarias, puede cargar los datos (muestreados o con características) en un blob de Azure y consumirlos en Aprendizaje automático de Azure, mediante los siguientes pasos. Tenga en cuenta que también se pueden crear características adicionales en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b7b45-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="b7b45-141">Escriba la trama de datos en el archivo local</span><span class="sxs-lookup"><span data-stu-id="b7b45-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="b7b45-142">Cargue los datos en el blob de Azure como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b7b45-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="b7b45-143">Ahora se pueden leer los datos del blob mediante el módulo [Importar datos][import-data] de Azure Machine Learning, como se muestra en la pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="b7b45-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![lector de blobs][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

