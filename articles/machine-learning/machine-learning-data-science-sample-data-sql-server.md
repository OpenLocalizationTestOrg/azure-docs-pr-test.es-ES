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
# <span data-ttu-id="95ae2-103"><a name="heading"></a>Muestreo de datos en SQL Server en Azure</span><span class="sxs-lookup"><span data-stu-id="95ae2-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="95ae2-104">Este documento, muestra cómo se almacenan los datos de toosample en SQL Server en Azure con SQL u Hola lenguaje de programación Python.</span><span class="sxs-lookup"><span data-stu-id="95ae2-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="95ae2-105">También muestra cómo toomove los datos de ejemplo en aprendizaje automático de Azure Guardando archivo tooa, cargarlo tooan blobs de Azure y, a continuación, leerlo en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="95ae2-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="95ae2-106">muestreo de Python de Hello usa hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC biblioteca tooconnect tooSQL Server en Azure y hello [Pandas](http://pandas.pydata.org/) muestreo de biblioteca toodo Hola.</span><span class="sxs-lookup"><span data-stu-id="95ae2-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="95ae2-107">código de SQL de ejemplo de Hola en este documento se da por supuesto que Hola datos están en un servidor SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="95ae2-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="95ae2-108">Si no es así, consulte demasiado[mover datos tooSQL Server en Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tema para obtener instrucciones sobre cómo toomove su tooSQL datos del servidor en Azure.</span><span class="sxs-lookup"><span data-stu-id="95ae2-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="95ae2-109">siguiente Hello **menú** vincula tootopics que describen cómo toosample datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="95ae2-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="95ae2-110">**¿Por qué realizar un muestreo de los datos?**</span><span class="sxs-lookup"><span data-stu-id="95ae2-110">**Why sample your data?**</span></span>
<span data-ttu-id="95ae2-111">Si piensa tooanalyze de conjunto de datos de hello es grande, normalmente es un tooreduce de datos de ejemplo toodown Hola buena idea tooa más pequeño pero representativo y más fáciles de administrar el tamaño.</span><span class="sxs-lookup"><span data-stu-id="95ae2-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="95ae2-112">Esto facilita la comprensión y exploración de los datos, y el diseño de características.</span><span class="sxs-lookup"><span data-stu-id="95ae2-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="95ae2-113">Su función en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) es tooenable la creación de prototipos rápida de las funciones de procesamiento de datos de Hola y modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="95ae2-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="95ae2-114">Esta tarea de muestreo es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="95ae2-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="95ae2-115"><a name="SQL"></a>Uso de SQL</span><span class="sxs-lookup"><span data-stu-id="95ae2-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="95ae2-116">Esta sección describen varios métodos que utilizan SQL tooperform un muestreo aleatorio simple con datos de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="95ae2-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="95ae2-117">Elija un método basado en el tamaño de los datos y su distribución.</span><span class="sxs-lookup"><span data-stu-id="95ae2-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="95ae2-118">Hola los dos elementos a continuación muestran cómo toouse newid en SQL Server tooperform Hola muestreo.</span><span class="sxs-lookup"><span data-stu-id="95ae2-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="95ae2-119">Hello método que elija depende de cómo aleatorio desea toobe de ejemplo de Hola (pk_id en el siguiente código de ejemplo de Hola se supone toobe una clave principal generada automáticamente).</span><span class="sxs-lookup"><span data-stu-id="95ae2-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="95ae2-120">Muestra aleatoria menos estricta</span><span class="sxs-lookup"><span data-stu-id="95ae2-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="95ae2-121">Muestra más aleatoria</span><span class="sxs-lookup"><span data-stu-id="95ae2-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="95ae2-122">Tablesample se puede usar para el muestreo, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="95ae2-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="95ae2-123">Esto se puede un enfoque más adecuado si el tamaño de los datos es grande (suponiendo que no está correlacionados datos en distintas páginas) y para hello consulta toocomplete en un tiempo razonable.</span><span class="sxs-lookup"><span data-stu-id="95ae2-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="95ae2-124">Puede explorar y generar características de los datos muestreados almacenándolos en una nueva tabla</span><span class="sxs-lookup"><span data-stu-id="95ae2-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="95ae2-125"><a name="sql-aml"></a>Conexión tooAzure aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="95ae2-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="95ae2-126">Puede usar directamente las consultas de ejemplo de Hola anteriormente en hello aprendizaje automático de Azure [importar datos] [ import-data] datos de ejemplo toodown Hola de módulo en hello volar y ponerla en un experimento de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="95ae2-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="95ae2-127">A continuación se muestra una captura de pantalla de usar Hola lector módulo tooread Hola muestreada datos:</span><span class="sxs-lookup"><span data-stu-id="95ae2-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![lector sql][1]

## <span data-ttu-id="95ae2-129"><a name="python"></a>Utilizando el lenguaje de programación Python Hola</span><span class="sxs-lookup"><span data-stu-id="95ae2-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="95ae2-130">En esta sección se muestra el uso de hello [pyodbc biblioteca](https://code.google.com/p/pyodbc/) tooestablish un ODBC conectarse tooa base de datos SQL server en Python.</span><span class="sxs-lookup"><span data-stu-id="95ae2-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="95ae2-131">cadena de conexión de base de datos de Hello es como sigue: (reemplace servername, dbname, username y password por la configuración):</span><span class="sxs-lookup"><span data-stu-id="95ae2-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="95ae2-132">Hola [Pandas](http://pandas.pydata.org/) biblioteca de Python proporciona un amplio conjunto de estructuras de datos y herramientas de análisis de datos para la manipulación de datos para la programación de Python.</span><span class="sxs-lookup"><span data-stu-id="95ae2-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="95ae2-133">código de Hello siguiente lee un ejemplo de 0,1% de los datos de Hola de una tabla de base de datos SQL de Azure en datos Pandas:</span><span class="sxs-lookup"><span data-stu-id="95ae2-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="95ae2-134">Ahora puede trabajar con datos de hello muestreada en la trama de datos de Pandas Hola.</span><span class="sxs-lookup"><span data-stu-id="95ae2-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="95ae2-135"><a name="python-aml"></a>Conexión tooAzure aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="95ae2-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="95ae2-136">Puede usar hello siguiente ejemplo código toosave Hola datos muestreados abajo tooa archivo y cargarlo tooan blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="95ae2-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="95ae2-137">datos de Hola de blob de hello pueden directamente leerse en un experimento de aprendizaje de máquina de Azure mediante hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="95ae2-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="95ae2-138">pasos de Hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="95ae2-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="95ae2-139">Escribir en el archivo local tooa del marco de datos de hello pandas</span><span class="sxs-lookup"><span data-stu-id="95ae2-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="95ae2-140">Cargar archivo local tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="95ae2-140">Upload local file tooAzure blob</span></span>
   
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
3. <span data-ttu-id="95ae2-141">Leer datos de blob de Azure mediante el aprendizaje automático de Azure [importar datos] [ import-data] módulo tal y como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="95ae2-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![lector de blobs][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="95ae2-143">Hola proceso de ciencia de datos de equipo en el ejemplo de acción</span><span class="sxs-lookup"><span data-stu-id="95ae2-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="95ae2-144">Para obtener un ejemplo de tutorial de extremo a extremo de hello proceso de ciencia de datos de equipo una con un conjunto de datos pública, consulte [proceso de ciencia de datos de equipo en acción: usar SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="95ae2-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
