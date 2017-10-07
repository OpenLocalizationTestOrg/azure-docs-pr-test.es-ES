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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Exploración de datos en el almacenamiento de blobs de Azure con Pandas
Este documento cubre cómo tooexplore datos que se almacenan en Azure blob contenedor mediante [Pandas](http://pandas.pydata.org/) paquete de Python.

siguiente Hello **menú** vincula tootopics que describen cómo toouse herramientas tooexplore datos desde varios entornos de almacenamiento. Esta tarea es un paso en hello [proceso de ciencia de datos]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que ha:

* Creado una cuenta de almacenamiento de Azure. Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Almacenó los datos en una cuenta de almacenamiento de blobs de Azure. Si necesita instrucciones, consulte [tooand de mover datos desde el almacenamiento de Azure](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Cargar datos de hello en una trama de datos de Pandas
tooexplore y manipular un conjunto de datos, primero debe descargarse de hello blob origen tooa archivo local, que, a continuación, se pueden cargar en una trama de datos de Pandas. A continuación, incluimos hello toofollow de pasos para realizar este procedimiento:

1. Descargar datos Hola de Azure blob con hello siguiendo el ejemplo de código de Python mediante servicio de blobs. Reemplace la variable de Hola Hola después el código con los valores específicos: 
   
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

## <a name="blob-dataexploration"></a>Ejemplos de exploración de datos con Pandas
Estos son algunos ejemplos de formas de datos de tooexplore mediante Pandas:

1. Inspeccionar hello **número de filas y columnas** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Inspeccionar** Hola algunos primeros o últimos **filas** Hola siguiendo el conjunto de datos:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Comprobar hello **tipo de datos** cada columna se importó como mediante el siguiente código de ejemplo de Hola
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Comprobar hello **estadísticas básicas** para columnas Hola de Hola conjunto de datos como se indica a continuación.
   
        dataframe_blobdata.describe()
5. Busque Hola número de entradas para cada valor de columna como se indica a continuación.
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Recuento de valores que faltan** frente a un número real de entradas de cada columna mediante el siguiente código de ejemplo de Hola Hola
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Si tiene **valores que faltan** para una columna concreta de datos de hello, puede arrastrar como se indica a continuación:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Valores que faltan de otra manera tooreplace es con la función de modo de hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Crear un **histograma** trazado mediante un número variable de distribución de hello tooplot de cubos de una variable    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Mire **correlaciones** entre las variables utilizando un scatterplot u Hola integrados correlation, función
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

