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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Creación de características para los datos de almacenamiento de blobs de Azure mediante Panda
Este documento muestra cómo las características de los datos que se almacenan en el contenedor de blobs de Azure mediante hello toocreate [Pandas](http://pandas.pydata.org/) paquete de Python. Después de esquematizar cómo datos de hello tooload dentro de una trama de datos de Panda, muestra cómo toogenerate las características de categorías mediante scripts de Python con valores de indicador y características de discretización.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Esto **menú** vincula tootopics que describen cómo toocreate características para los datos en varios entornos. Esta tarea es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que ja creado una cuenta de almacenamiento de blobs de Azure y que ha almacenado los datos ahí. Si necesita instrucciones tooset una cuenta, consulte [crear una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Cargar datos de hello en una trama de datos Pandas
En orden toodo explorar y manipular un conjunto de datos, debe descargarse de hello blob origen tooa archivo local que, a continuación, se pueden cargar en una trama de datos de Pandas. A continuación, incluimos hello toofollow de pasos para realizar este procedimiento:

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

## <a name="blob-featuregen"></a>Generación de características
Hola dos secciones siguientes mostrar cómo toogenerate las características de categorías con valores de indicador y discretización características mediante scripts de Python.

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
3. Ahora puede leer datos de Hola de hello blob mediante Hola aprendizaje automático de Azure [importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) módulo tal y como se muestra en la pantalla de bienvenida a continuación:

![lector de blobs](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

