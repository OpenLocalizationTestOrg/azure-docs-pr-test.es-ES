---
title: aaaSample datos de SQL Server en Azure | Documentos de Microsoft
description: Muestreo de datos en SQL Server en Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Muestreo de datos en SQL Server en Azure
Este documento, muestra cómo se almacenan los datos de toosample en SQL Server en Azure con SQL u Hola lenguaje de programación Python. También muestra cómo toomove los datos de ejemplo en aprendizaje automático de Azure Guardando archivo tooa, cargarlo tooan blobs de Azure y, a continuación, leerlo en estudio de aprendizaje automático de Azure.

muestreo de Python de Hello usa hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC biblioteca tooconnect tooSQL Server en Azure y hello [Pandas](http://pandas.pydata.org/) muestreo de biblioteca toodo Hola.

> [!NOTE]
> código de SQL de ejemplo de Hola en este documento se da por supuesto que Hola datos están en un servidor SQL Server en Azure. Si no es así, consulte demasiado[mover datos tooSQL Server en Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tema para obtener instrucciones sobre cómo toomove su tooSQL datos del servidor en Azure.
> 
> 

siguiente Hello **menú** vincula tootopics que describen cómo toosample datos desde varios entornos de almacenamiento. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**¿Por qué realizar un muestreo de los datos?**
Si piensa tooanalyze de conjunto de datos de hello es grande, normalmente es un tooreduce de datos de ejemplo toodown Hola buena idea tooa más pequeño pero representativo y más fáciles de administrar el tamaño. Esto facilita la comprensión y exploración de los datos, y el diseño de características. Su función en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) es tooenable la creación de prototipos rápida de las funciones de procesamiento de datos de Hola y modelos de aprendizaje automático.

Esta tarea de muestreo es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Uso de SQL
Esta sección describen varios métodos que utilizan SQL tooperform un muestreo aleatorio simple con datos de hello en la base de datos de Hola. Elija un método basado en el tamaño de los datos y su distribución.

Hola los dos elementos a continuación muestran cómo toouse newid en SQL Server tooperform Hola muestreo. Hello método que elija depende de cómo aleatorio desea toobe de ejemplo de Hola (pk_id en el siguiente código de ejemplo de Hola se supone toobe una clave principal generada automáticamente).

1. Muestra aleatoria menos estricta
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Muestra más aleatoria 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Tablesample se puede usar para el muestreo, como se muestra a continuación. Esto se puede un enfoque más adecuado si el tamaño de los datos es grande (suponiendo que no está correlacionados datos en distintas páginas) y para hello consulta toocomplete en un tiempo razonable.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> Puede explorar y generar características de los datos muestreados almacenándolos en una nueva tabla
> 
> 

### <a name="sql-aml"></a>Conexión tooAzure aprendizaje automático
Puede usar directamente las consultas de ejemplo de Hola anteriormente en hello aprendizaje automático de Azure [importar datos] [ import-data] datos de ejemplo toodown Hola de módulo en hello volar y ponerla en un experimento de aprendizaje automático de Azure. A continuación se muestra una captura de pantalla de usar Hola lector módulo tooread Hola muestreada datos:

![lector sql][1]

## <a name="python"></a>Utilizando el lenguaje de programación Python Hola
En esta sección se muestra el uso de hello [pyodbc biblioteca](https://code.google.com/p/pyodbc/) tooestablish un ODBC conectarse tooa base de datos SQL server en Python. cadena de conexión de base de datos de Hello es como sigue: (reemplace servername, dbname, username y password por la configuración):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hola [Pandas](http://pandas.pydata.org/) biblioteca de Python proporciona un amplio conjunto de estructuras de datos y herramientas de análisis de datos para la manipulación de datos para la programación de Python. código de Hello siguiente lee un ejemplo de 0,1% de los datos de Hola de una tabla de base de datos SQL de Azure en datos Pandas:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Ahora puede trabajar con datos de hello muestreada en la trama de datos de Pandas Hola. 

### <a name="python-aml"></a>Conexión tooAzure aprendizaje automático
Puede usar hello siguiente ejemplo código toosave Hola datos muestreados abajo tooa archivo y cargarlo tooan blobs de Azure. datos de Hola de blob de hello pueden directamente leerse en un experimento de aprendizaje de máquina de Azure mediante hello [importar datos] [ import-data] módulo. pasos de Hello son los siguientes: 

1. Escribir en el archivo local tooa del marco de datos de hello pandas
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Cargar archivo local tooAzure blob
   
        from azure.storage import BlobService
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
3. Leer datos de blob de Azure mediante el aprendizaje automático de Azure [importar datos] [ import-data] módulo tal y como se muestra en la siguiente captura de pantalla de hello:

![lector de blobs][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Hola proceso de ciencia de datos de equipo en el ejemplo de acción
Para obtener un ejemplo de tutorial de extremo a extremo de hello proceso de ciencia de datos de equipo una con un conjunto de datos pública, consulte [proceso de ciencia de datos de equipo en acción: usar SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
