---
title: "Exploración de datos en una máquina virtual de SQL Server de Azure | Microsoft Docs"
description: "Exploración de datos y creación de características en una máquina virtual de SQL Server de Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="75de8-103"><a name="heading"></a>Proceso de datos en una máquina virtual de SQL Server en Azure</span><span class="sxs-lookup"><span data-stu-id="75de8-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="75de8-104">En este documento se aborda cómo explorar datos y generar características para los datos almacenados en una VM de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="75de8-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="75de8-105">Esto puede hacerse mediante la administración de datos usando SQL o mediante un lenguaje de programación como Python.</span><span class="sxs-lookup"><span data-stu-id="75de8-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="75de8-106">En las instrucciones SQL de ejemplo de este documento se supone que los datos están en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75de8-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="75de8-107">Si no lo están, consulte el mapa de proceso de ciencia de datos en la nube para obtener información sobre cómo mover los datos a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75de8-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="75de8-108"><a name="SQL"></a>Uso de SQL</span><span class="sxs-lookup"><span data-stu-id="75de8-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="75de8-109">En esta sección, se describen las siguientes tareas de tratamiento de datos mediante SQL:</span><span class="sxs-lookup"><span data-stu-id="75de8-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="75de8-110">Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="75de8-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="75de8-111">Generación de características</span><span class="sxs-lookup"><span data-stu-id="75de8-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="75de8-112"><a name="sql-dataexploration"></a>Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="75de8-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="75de8-113">A continuación se muestran algunos scripts de SQL de ejemplo que se pueden usar para explorar los almacenes de datos en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75de8-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="75de8-114">Para obtener un ejemplo práctico, puede usar el conjunto de datos [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) y consultar el IPNB denominado [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) (Tratamiento de datos de la ciudad de Nueva York mediante IPython Notebook y SQL Server), que ofrece un tutorial completo.</span><span class="sxs-lookup"><span data-stu-id="75de8-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="75de8-115">Obtener el número de observaciones por día</span><span class="sxs-lookup"><span data-stu-id="75de8-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="75de8-116">Obtenga los niveles de una columna de categorías</span><span class="sxs-lookup"><span data-stu-id="75de8-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="75de8-117">Obtener el número de niveles de combinación de dos columnas de categorías</span><span class="sxs-lookup"><span data-stu-id="75de8-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="75de8-118">Obtener la distribución para columnas numéricas</span><span class="sxs-lookup"><span data-stu-id="75de8-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="75de8-119"><a name="sql-featuregen"></a>Generación de características</span><span class="sxs-lookup"><span data-stu-id="75de8-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="75de8-120">En esta sección, se describen formas de generar características mediante SQL:</span><span class="sxs-lookup"><span data-stu-id="75de8-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="75de8-121">Generación de características basadas en recuentos</span><span class="sxs-lookup"><span data-stu-id="75de8-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="75de8-122">Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="75de8-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="75de8-123">Implementación de las características de una sola columna</span><span class="sxs-lookup"><span data-stu-id="75de8-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="75de8-124">Cuando genere características adicionales, puede agregarlas como columnas a la tabla existente o crear una nueva tabla con las características adicionales y la clave principal, que se pueden combinar con la tabla original.</span><span class="sxs-lookup"><span data-stu-id="75de8-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="75de8-125"><a name="sql-countfeature"></a>Generación de características basadas en recuentos</span><span class="sxs-lookup"><span data-stu-id="75de8-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="75de8-126">Los ejemplos siguientes muestran dos formas de generar características de recuento.</span><span class="sxs-lookup"><span data-stu-id="75de8-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="75de8-127">El primer método usa la suma condicional y el segundo utiliza la cláusula 'where'.</span><span class="sxs-lookup"><span data-stu-id="75de8-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="75de8-128">Estos pueden entonces combinarse con la tabla original (con columnas de clave principal) para disponer de características de recuento junto con los datos originales.</span><span class="sxs-lookup"><span data-stu-id="75de8-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="75de8-129"><a name="sql-binningfeature"></a>Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="75de8-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="75de8-130">En el ejemplo siguiente se muestra cómo generar características discretizadas mediante la discretización (con cinco discretizaciones) de una columna numérica que puede usarse en su lugar como una característica:</span><span class="sxs-lookup"><span data-stu-id="75de8-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="75de8-131"><a name="sql-featurerollout"></a>Implementación de las características de una sola columna</span><span class="sxs-lookup"><span data-stu-id="75de8-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="75de8-132">En esta sección, se muestra cómo se implementa una sola columna de una tabla para generar características adicionales.</span><span class="sxs-lookup"><span data-stu-id="75de8-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="75de8-133">En el ejemplo se supone que hay una columna de latitud o longitud en la tabla a partir de la cual está intentando generar características.</span><span class="sxs-lookup"><span data-stu-id="75de8-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="75de8-134">Aquí se incluye un breve manual sobre los datos de ubicación de latitud y longitud (extraído de stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)(¿Cómo medir la precisión de la latitud y la longitud?)).</span><span class="sxs-lookup"><span data-stu-id="75de8-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="75de8-135">Resulta útil para comprender bien todo antes de caracterizar el campo de ubicación:</span><span class="sxs-lookup"><span data-stu-id="75de8-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="75de8-136">La señal indica si estamos en el norte o sur, y este u oeste del mundo.</span><span class="sxs-lookup"><span data-stu-id="75de8-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="75de8-137">Un dígito de las centenas distinto de cero indica que se usa la longitud y no la latitud.</span><span class="sxs-lookup"><span data-stu-id="75de8-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="75de8-138">El dígito de las decenas ofrece una posición a aproximadamente 1.000 kilómetros.</span><span class="sxs-lookup"><span data-stu-id="75de8-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="75de8-139">Nos brinda información útil sobre el continente u océano en el que nos encontramos.</span><span class="sxs-lookup"><span data-stu-id="75de8-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="75de8-140">El dígito de las unidades (un grado decimal) indica una posición de hasta 111 kilómetros (60 millas náuticas, aproximadamente 69 millas).</span><span class="sxs-lookup"><span data-stu-id="75de8-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="75de8-141">Puede informarnos aproximadamente del estado grande o país en que nos encontramos.</span><span class="sxs-lookup"><span data-stu-id="75de8-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="75de8-142">La primera posición decimal tiene un valor de hasta 11,1 km: puede distinguir la posición de una ciudad grande de otra ciudad grande vecina.</span><span class="sxs-lookup"><span data-stu-id="75de8-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="75de8-143">La segundo posición decimal tiene un valor de hasta 1,1 km: puede separar un pueblo del siguiente.</span><span class="sxs-lookup"><span data-stu-id="75de8-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="75de8-144">La tercera posición decimal tiene un valor de hasta 110 m: puede identificar un campo agrícola extenso o campus universitario.</span><span class="sxs-lookup"><span data-stu-id="75de8-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="75de8-145">La cuarta posición decimal tiene un valor de hasta 11 m: puede identificar una parcela de tierra.</span><span class="sxs-lookup"><span data-stu-id="75de8-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="75de8-146">Es comparable a la precisión típica de una unidad GPS sin corregir y sin interferencias.</span><span class="sxs-lookup"><span data-stu-id="75de8-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="75de8-147">La quinta posición decimal tiene un valor de hasta 1,1 m: puede distinguir entre distintos árboles.</span><span class="sxs-lookup"><span data-stu-id="75de8-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="75de8-148">Solo es posible conseguir una precisión de este nivel con unidades GPS comerciales con corrección diferencial.</span><span class="sxs-lookup"><span data-stu-id="75de8-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="75de8-149">La sexta posición decimal tiene un valor de hasta 0,11 m: puede usarse para diseñar estructuras en detalle, para el diseño de paisajes o la construcción de carreteras.</span><span class="sxs-lookup"><span data-stu-id="75de8-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="75de8-150">Debería ser más que suficiente para realizar el seguimiento de los movimientos de glaciares y ríos.</span><span class="sxs-lookup"><span data-stu-id="75de8-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="75de8-151">Esto se consigue al tomar medidas meticulosas con GPS, como GPS corregido de forma diferencial.</span><span class="sxs-lookup"><span data-stu-id="75de8-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="75de8-152">La información de ubicación se puede caracterizar como sigue, con diferencias entre la información de región, ubicación y ciudad.</span><span class="sxs-lookup"><span data-stu-id="75de8-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="75de8-153">Tenga en cuenta que también es posible llamar a un punto de conexión de REST, como la API de mapas de Bing disponible en [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) (Encontrar una ubicación por punto) para obtener la información de la región o el distrito.</span><span class="sxs-lookup"><span data-stu-id="75de8-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="75de8-154">Estas características basadas en ubicación se pueden usar aún más para generar características de recuento adicionales, tal y como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="75de8-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="75de8-155">Puede insertar mediante programación los registros con el lenguaje que prefiera.</span><span class="sxs-lookup"><span data-stu-id="75de8-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="75de8-156">Es posible que deba insertar los datos en fragmentos para mejorar el rendimiento de escritura (para obtener un ejemplo de cómo obtener esto mediante pyodbc, consulte [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)(Un ejemplo Hola a todos para acceder a SQLServer con python)).</span><span class="sxs-lookup"><span data-stu-id="75de8-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="75de8-157">Otra alternativa consiste en insertar datos en la base de datos mediante la [utilidad BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="75de8-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="75de8-158"><a name="sql-aml"></a>Conexión con Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="75de8-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="75de8-159">La característica recién generada se puede agregar como una columna a una tabla existente o se puede almacenar en una tabla nueva y combinar con la tabla original para el aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="75de8-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="75de8-160">Es posible generar o tener acceso a las características si ya se han creado, mediante el módulo [Importar datos][import-data] en Azure Machine Learning, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="75de8-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![Lectores de azureml][1] 

## <span data-ttu-id="75de8-162"><a name="python"></a>Uso de un lenguaje de programación como Python</span><span class="sxs-lookup"><span data-stu-id="75de8-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="75de8-163">Usar Python para generar explorar datos y generar características cuando los datos están en SQL Server es parecido a procesar los datos en blobs de Azure mediante Python, como se documenta en [Proceso de datos de blobs de Azure en su entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="75de8-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="75de8-164">Los datos deben cargarse desde la base de datos en una trama de datos de Pandas y, a continuación, se pueden procesar aún más.</span><span class="sxs-lookup"><span data-stu-id="75de8-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="75de8-165">Se documenta el proceso de conexión a la base de datos y carga de los datos en la trama de datos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="75de8-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="75de8-166">El formato de cadena de conexión siguiente puede usarse para conectarse a una base de datos de SQL Server desde Python mediante pyodbc (reemplace servername, dbname, username y password con sus valores específicos):</span><span class="sxs-lookup"><span data-stu-id="75de8-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="75de8-167">La [biblioteca Pandas](http://pandas.pydata.org/) en Python ofrece un amplio conjunto de herramientas de análisis de datos y estructuras de datos para la manipulación de datos para la programación en Python.</span><span class="sxs-lookup"><span data-stu-id="75de8-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="75de8-168">El código siguiente lee los resultados que se devuelven desde una base de datos de SQL Server en una trama de datos de Pandas:</span><span class="sxs-lookup"><span data-stu-id="75de8-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="75de8-169">Ya puede trabajar con la trama de datos de Pandas como se explica en el artículo [Proceso de datos de blobs de Azure en su entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="75de8-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="75de8-170">Ejemplo de ciencia de datos de Azure en acción</span><span class="sxs-lookup"><span data-stu-id="75de8-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="75de8-171">Para obtener un ejemplo de tutorial completo del Proceso de ciencia de datos de Azure mediante un conjunto de datos público, consulte [Proceso de ciencia de datos de Azure en acción](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="75de8-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

