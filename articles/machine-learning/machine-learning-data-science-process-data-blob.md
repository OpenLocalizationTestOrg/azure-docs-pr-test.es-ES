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
# <a name="heading"></a>Proceso de datos del blob de Azure con análisis avanzado
En este documento se trata la exploración de datos y generación de características a partir de los datos almacenados en Almacenamiento de blobs de Azure. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Cargar datos de hello en una trama de datos Pandas
En orden tooexplore y manipular un conjunto de datos, debe descargarse de hello blob origen tooa archivo local que, a continuación, se pueden cargar en una trama de datos de Pandas. A continuación, incluimos hello toofollow de pasos para realizar este procedimiento:

1. Descargar datos Hola de Azure blob con hello después el código Python de ejemplo con servicio de blobs. Reemplace la variable de hello en el código de hello a continuación con los valores específicos: 
   
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
2. Leer datos de hello en una trama de datos Pandas de hello descargan el archivo.
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Ahora va a datos de hello tooexplore listo y genera características en este conjunto de datos.

## <a name="blob-dataexploration"></a>Exploración de datos
Estos son algunos ejemplos de formas de datos de tooexplore mediante Pandas:

1. Inspeccionar Hola número de filas y columnas 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Inspeccionar Hola primero o último algunas filas de conjunto de datos de hello como sigue:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Comprobar tipo de datos de hello que cada columna se importó como mediante el siguiente código de ejemplo de Hola
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Comprobar estadísticas básicas de Hola para las columnas de Hola Hola conjunto de datos como se indica a continuación.
   
        dataframe_blobdata.describe()
5. Busque Hola número de entradas para cada valor de columna como se indica a continuación.
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Recuento de valores que faltan frente a un número real de entradas de cada columna mediante el siguiente código de ejemplo de Hola Hola
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Si tiene los valores que faltan para una columna específica en los datos de hello, puede colocarlas como sigue:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Valores que faltan de otra manera tooreplace es con la función de modo de hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Crear un gráfico de histograma con un número variable de distribución de hello tooplot de cubos de una variable    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Examine las correlaciones entre las variables utilizando un scatterplot u Hola integrados correlation, función
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Generación de características
Es posible generar características con Python de la siguiente manera:

### <a name="blob-countfeature"></a>Generación de características basada en el valor de indicador
Las características de categorías se pueden crear como sigue:

1. Inspeccionar la distribución de Hola de columna de categorías de hello:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Generar valores de indicador para cada uno de los valores de columna de Hola
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Unirse a la columna de indicador de hello con trama de datos original de Hola 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Quitar la propia variable original de hello:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Generación de características de discretización
Para generar características discretizadas, se procede de la siguiente manera:

1. Agregar una secuencia de columnas toobin una columna numérica
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Convierte la secuencia de tooa discretización de las variables booleanas
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Por último, las variables ficticias de Hola de combinación nuevamente toohello trama de datos original
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <a name="sql-featuregen"></a>Hacer copia de escribir datos blob tooAzure y consume en aprendizaje automático de Azure
Una vez haya explorar datos hello y crea Hola características necesarias, puede cargar datos de hello (muestrear o caracterizará) tooan Azure blob y usarla en aprendizaje automático de Azure con hello pasos: tenga en cuenta que las características adicionales se pueden crear en hello Azure estudio de aprendizaje automático también. 

1. Escribir en el archivo de hello datos marco toolocal
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Cargar blob de hello datos tooAzure como se indica a continuación:
   
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
3. Ahora puede leer datos de Hola de hello blob mediante Hola aprendizaje automático de Azure [importar datos] [ import-data] módulo tal y como se muestra en la pantalla de bienvenida a continuación:

![lector de blobs][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

