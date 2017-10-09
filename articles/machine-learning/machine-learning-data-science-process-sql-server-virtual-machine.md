---
title: "aaaExplore datos en una máquina virtual de SQL Server en Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="3ab73-103"><a name="heading"></a>Proceso de datos en una máquina virtual de SQL Server en Azure</span><span class="sxs-lookup"><span data-stu-id="3ab73-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="3ab73-104">Este documento cubre cómo tooexplore datos y generar características de los datos almacenados en una VM de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="3ab73-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="3ab73-105">Esto puede hacerse mediante la administración de datos usando SQL o mediante un lenguaje de programación como Python.</span><span class="sxs-lookup"><span data-stu-id="3ab73-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="3ab73-106">instrucciones de SQL de ejemplo de Hola en este documento se suponen que los datos están en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3ab73-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="3ab73-107">Si no es así, consulte cómo toohello nube datos ciencia proceso mapa toolearn toomove su tooSQL de datos servidor.</span><span class="sxs-lookup"><span data-stu-id="3ab73-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="3ab73-108"><a name="SQL"></a>Uso de SQL</span><span class="sxs-lookup"><span data-stu-id="3ab73-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="3ab73-109">Describimos Hola después problemas con tareas de datos en esta sección con SQL:</span><span class="sxs-lookup"><span data-stu-id="3ab73-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="3ab73-110">Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="3ab73-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="3ab73-111">Generación de características</span><span class="sxs-lookup"><span data-stu-id="3ab73-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="3ab73-112"><a name="sql-dataexploration"></a>Exploración de datos</span><span class="sxs-lookup"><span data-stu-id="3ab73-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="3ab73-113">Estos son algunos scripts SQL de ejemplo que pueden ser utilizados tooexplore almacenes de datos en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3ab73-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="3ab73-114">Para obtener un ejemplo práctico, puede usar hello [conjunto de datos de Nueva York Taxi](http://www.andresmh.com/nyctaxitrips/) y consulte toohello IPNB titulada [datos NYC problemas con mediante el Bloc de notas de IPython y SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para un tutorial to-end.</span><span class="sxs-lookup"><span data-stu-id="3ab73-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="3ab73-115">Obtener el recuento de Hola de observaciones por día</span><span class="sxs-lookup"><span data-stu-id="3ab73-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="3ab73-116">Obtener niveles de hello en una columna de categorías</span><span class="sxs-lookup"><span data-stu-id="3ab73-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="3ab73-117">Obtener número de Hola de niveles de combinación de dos columnas de categorías</span><span class="sxs-lookup"><span data-stu-id="3ab73-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="3ab73-118">Obtener la distribución de Hola para columnas numéricas</span><span class="sxs-lookup"><span data-stu-id="3ab73-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="3ab73-119"><a name="sql-featuregen"></a>Generación de características</span><span class="sxs-lookup"><span data-stu-id="3ab73-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="3ab73-120">En esta sección, se describen formas de generar características mediante SQL:</span><span class="sxs-lookup"><span data-stu-id="3ab73-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="3ab73-121">Generación de características basadas en recuentos</span><span class="sxs-lookup"><span data-stu-id="3ab73-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="3ab73-122">Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="3ab73-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="3ab73-123">Implementar características de Hola de una sola columna</span><span class="sxs-lookup"><span data-stu-id="3ab73-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="3ab73-124">Una vez que generar características adicionales, puede agregarlas como tabla de columnas toohello existente o crear una nueva tabla con características adicionales de Hola y la clave principal, que puede combinarse con la tabla original de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab73-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="3ab73-125"><a name="sql-countfeature"></a>Generación de características basadas en recuentos</span><span class="sxs-lookup"><span data-stu-id="3ab73-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="3ab73-126">Hello en los ejemplos siguientes muestran dos maneras de generar características de recuento.</span><span class="sxs-lookup"><span data-stu-id="3ab73-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="3ab73-127">Hola primero usa suma condicional y el segundo método utiliza de Hola Hola cláusula 'where'.</span><span class="sxs-lookup"><span data-stu-id="3ab73-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="3ab73-128">Estos, a continuación, pueden combinarse con hello original (con columnas de clave principal) toohave recuento características para tablas junto con los datos originales de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab73-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="3ab73-129"><a name="sql-binningfeature"></a>Generación de características de discretización</span><span class="sxs-lookup"><span data-stu-id="3ab73-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="3ab73-130">Hello en el ejemplo siguiente se muestra cómo toogenerate había discretizado características mediante discretización (con cinco ubicaciones) una columna numérica que puede utilizarse como una característica en su lugar:</span><span class="sxs-lookup"><span data-stu-id="3ab73-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="3ab73-131"><a name="sql-featurerollout"></a>Implementar características de Hola de una sola columna</span><span class="sxs-lookup"><span data-stu-id="3ab73-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="3ab73-132">En esta sección, demostraremos cómo tooroll espera una sola columna en una tabla toogenerate más características.</span><span class="sxs-lookup"><span data-stu-id="3ab73-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="3ab73-133">ejemplo de Hola se da por supuesto que hay una columna de latitud o longitud de tabla Hola desde el que está tratando de toogenerate características.</span><span class="sxs-lookup"><span data-stu-id="3ab73-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="3ab73-134">Aquí es un manual breve sobre los datos de ubicación de latitud y longitud (con los recursos de stackoverflow [cómo toomeasure Hola precisión de latitud y longitud?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="3ab73-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="3ab73-135">Esto es útil toounderstand antes de campo de ubicación de hello featurizing:</span><span class="sxs-lookup"><span data-stu-id="3ab73-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="3ab73-136">inicio de sesión de Hello nos dice si estamos Norte o sur, este u oeste mundo Hola.</span><span class="sxs-lookup"><span data-stu-id="3ab73-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="3ab73-137">Un dígito de las centenas distinto de cero indica que se usa la longitud y no la latitud.</span><span class="sxs-lookup"><span data-stu-id="3ab73-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="3ab73-138">dígito de Hello decenas ofrece un tooabout posición 1.000 kilómetros.</span><span class="sxs-lookup"><span data-stu-id="3ab73-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="3ab73-139">Nos brinda información útil sobre el continente u océano en el que nos encontramos.</span><span class="sxs-lookup"><span data-stu-id="3ab73-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="3ab73-140">dígito de unidades de Hello (un grado decimal) ofrece una posición hacia arriba too111 kilómetros (60 millas náuticas, unos 69 millas).</span><span class="sxs-lookup"><span data-stu-id="3ab73-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="3ab73-141">Puede informarnos aproximadamente del estado grande o país en que nos encontramos.</span><span class="sxs-lookup"><span data-stu-id="3ab73-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="3ab73-142">Hola primer decimal merece una too11.1 km: puede distinguir la posición de Hola de una ciudad grande de una ciudad grande vecino.</span><span class="sxs-lookup"><span data-stu-id="3ab73-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="3ab73-143">Hola segundo decimal merece una too1.1 km: puede separar un pueblo de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="3ab73-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="3ab73-144">posición decimal de la tercera Hola merece la pena seguridad too110 m: puede identificar un campo agrícola grande o recinto institucional.</span><span class="sxs-lookup"><span data-stu-id="3ab73-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="3ab73-145">Hola cuarto decimal merece una too11 m: puede identificar un lote de tierra.</span><span class="sxs-lookup"><span data-stu-id="3ab73-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="3ab73-146">Es comparable toohello precisión típica de una unidad GPS no corregida y sin interferencias.</span><span class="sxs-lookup"><span data-stu-id="3ab73-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="3ab73-147">Hola quinto decimal inferior es que vale la pena hasta too1.1 m: que árboles distinguen entre sí.</span><span class="sxs-lookup"><span data-stu-id="3ab73-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="3ab73-148">Nivel de precisión toothis con unidades GPS comerciales solo se puede lograr con corrección diferencial.</span><span class="sxs-lookup"><span data-stu-id="3ab73-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="3ab73-149">posición decimal de la sexta Hola merece la pena seguridad m: too0.11 que ya puede utilizarla para diseñar estructuras en detalle, para diseñar los entornos, crear carreteras.</span><span class="sxs-lookup"><span data-stu-id="3ab73-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="3ab73-150">Debería ser más que suficiente para realizar el seguimiento de los movimientos de glaciares y ríos.</span><span class="sxs-lookup"><span data-stu-id="3ab73-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="3ab73-151">Esto se consigue al tomar medidas meticulosas con GPS, como GPS corregido de forma diferencial.</span><span class="sxs-lookup"><span data-stu-id="3ab73-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="3ab73-152">información de ubicación de Hello puede ser caracterizará como sigue, separar los región, la ubicación y la información de la ciudad.</span><span class="sxs-lookup"><span data-stu-id="3ab73-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="3ab73-153">Tenga en cuenta que también puede llamar a un extremo REST, como la API de Bing Maps disponibles en [buscar una ubicación de punto de](https://msdn.microsoft.com/library/ff701710.aspx) información de tooget Hola región/distrito.</span><span class="sxs-lookup"><span data-stu-id="3ab73-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

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

<span data-ttu-id="3ab73-154">Estas características basadas en la ubicación pueden ser más características de recuento adicionales toogenerate usado como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3ab73-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="3ab73-155">Puede insertar mediante programación los registros de hello mediante el lenguaje seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3ab73-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="3ab73-156">Puede que necesite tooinsert datos de hello en la eficacia de escritura de fragmentos tooimprove (para obtener un ejemplo de cómo toodo este uso pyodbc, consulte [tooaccess de ejemplo HelloWorld A SQL Server con python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="3ab73-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="3ab73-157">Otra alternativa es tooinsert base de datos de hello mediante hello [utilidad BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ab73-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="3ab73-158"><a name="sql-aml"></a>Conexión tooAzure aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="3ab73-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="3ab73-159">característica Hola recién generado puede agrega como una tabla existente de columna tooan o almacenado en una tabla nueva y estar combinada con la tabla original de hello para el aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="3ab73-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="3ab73-160">Características se pueden genera o acceder si ya ha creado, con hello [importar datos] [ import-data] módulo aprendizaje automático de Azure tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="3ab73-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![Lectores de azureml][1] 

## <span data-ttu-id="3ab73-162"><a name="python"></a>Uso de un lenguaje de programación como Python</span><span class="sxs-lookup"><span data-stu-id="3ab73-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="3ab73-163">Usar datos de Python tooexplore y generar características cuando hello datos están en SQL Server es datos tooprocessing similares en Azure blob mediante Python como se documenta en [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="3ab73-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="3ab73-164">datos de Hello toobe cargado desde la base de datos de hello en una trama de datos pandas es necesario y, a continuación, pueden seguir procesándose.</span><span class="sxs-lookup"><span data-stu-id="3ab73-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="3ab73-165">Se documente proceso de Hola de conexión de base de datos de toohello y carga datos de hello en la trama de datos de hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="3ab73-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="3ab73-166">Hola siguiendo el formato de cadena de conexión puede ser usado tooconnect base de datos de SQL Server de la tooa de Python mediante pyodbc (replace servername, dbname, nombre de usuario y contraseña con los valores específicos):</span><span class="sxs-lookup"><span data-stu-id="3ab73-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="3ab73-167">Hola [biblioteca Pandas](http://pandas.pydata.org/) en Python proporciona un amplio conjunto de estructuras de datos y herramientas de análisis de datos para la manipulación de datos para la programación de Python.</span><span class="sxs-lookup"><span data-stu-id="3ab73-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="3ab73-168">código de Hello siguiente lee devuelven resultados de Hola de una base de datos de SQL Server en una trama de datos de Pandas:</span><span class="sxs-lookup"><span data-stu-id="3ab73-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="3ab73-169">Ahora puede trabajar con la trama de datos de hello Pandas tal como se explicó en el artículo hello [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="3ab73-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="3ab73-170">Ejemplo de ciencia de datos de Azure en acción</span><span class="sxs-lookup"><span data-stu-id="3ab73-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="3ab73-171">Para obtener un ejemplo de tutorial de extremo a extremo de hello proceso de ciencia de datos de Azure con un conjunto de datos pública, consulte [proceso de ciencia de datos de Azure en acción](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="3ab73-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

