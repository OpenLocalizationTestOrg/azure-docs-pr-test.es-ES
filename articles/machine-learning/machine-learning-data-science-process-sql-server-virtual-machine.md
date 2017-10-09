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
# <a name="heading"></a>Proceso de datos en una máquina virtual de SQL Server en Azure
Este documento cubre cómo tooexplore datos y generar características de los datos almacenados en una VM de SQL Server en Azure. Esto puede hacerse mediante la administración de datos usando SQL o mediante un lenguaje de programación como Python.

> [!NOTE]
> instrucciones de SQL de ejemplo de Hola en este documento se suponen que los datos están en SQL Server. Si no es así, consulte cómo toohello nube datos ciencia proceso mapa toolearn toomove su tooSQL de datos servidor.
> 
> 

## <a name="SQL"></a>Uso de SQL
Describimos Hola después problemas con tareas de datos en esta sección con SQL:

1. [Exploración de datos](#sql-dataexploration)
2. [Generación de características](#sql-featuregen)

### <a name="sql-dataexploration"></a>Exploración de datos
Estos son algunos scripts SQL de ejemplo que pueden ser utilizados tooexplore almacenes de datos en SQL Server.

> [!NOTE]
> Para obtener un ejemplo práctico, puede usar hello [conjunto de datos de Nueva York Taxi](http://www.andresmh.com/nyctaxitrips/) y consulte toohello IPNB titulada [datos NYC problemas con mediante el Bloc de notas de IPython y SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para un tutorial to-end.
> 
> 

1. Obtener el recuento de Hola de observaciones por día
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Obtener niveles de hello en una columna de categorías
   
    `select  distinct <column_name> from <databasename>`
3. Obtener número de Hola de niveles de combinación de dos columnas de categorías 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Obtener la distribución de Hola para columnas numéricas
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>Generación de características
En esta sección, se describen formas de generar características mediante SQL:  

1. [Generación de características basadas en recuentos](#sql-countfeature)
2. [Generación de características de discretización](#sql-binningfeature)
3. [Implementar características de Hola de una sola columna](#sql-featurerollout)

> [!NOTE]
> Una vez que generar características adicionales, puede agregarlas como tabla de columnas toohello existente o crear una nueva tabla con características adicionales de Hola y la clave principal, que puede combinarse con la tabla original de Hola. 
> 
> 

### <a name="sql-countfeature"></a>Generación de características basadas en recuentos
Hello en los ejemplos siguientes muestran dos maneras de generar características de recuento. Hola primero usa suma condicional y el segundo método utiliza de Hola Hola cláusula 'where'. Estos, a continuación, pueden combinarse con hello original (con columnas de clave principal) toohave recuento características para tablas junto con los datos originales de Hola.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>Generación de características de discretización
Hello en el ejemplo siguiente se muestra cómo toogenerate había discretizado características mediante discretización (con cinco ubicaciones) una columna numérica que puede utilizarse como una característica en su lugar:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Implementar características de Hola de una sola columna
En esta sección, demostraremos cómo tooroll espera una sola columna en una tabla toogenerate más características. ejemplo de Hola se da por supuesto que hay una columna de latitud o longitud de tabla Hola desde el que está tratando de toogenerate características.

Aquí es un manual breve sobre los datos de ubicación de latitud y longitud (con los recursos de stackoverflow [cómo toomeasure Hola precisión de latitud y longitud?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)). Esto es útil toounderstand antes de campo de ubicación de hello featurizing:

* inicio de sesión de Hello nos dice si estamos Norte o sur, este u oeste mundo Hola.
* Un dígito de las centenas distinto de cero indica que se usa la longitud y no la latitud.
* dígito de Hello decenas ofrece un tooabout posición 1.000 kilómetros. Nos brinda información útil sobre el continente u océano en el que nos encontramos.
* dígito de unidades de Hello (un grado decimal) ofrece una posición hacia arriba too111 kilómetros (60 millas náuticas, unos 69 millas). Puede informarnos aproximadamente del estado grande o país en que nos encontramos.
* Hola primer decimal merece una too11.1 km: puede distinguir la posición de Hola de una ciudad grande de una ciudad grande vecino.
* Hola segundo decimal merece una too1.1 km: puede separar un pueblo de Hola a continuación.
* posición decimal de la tercera Hola merece la pena seguridad too110 m: puede identificar un campo agrícola grande o recinto institucional.
* Hola cuarto decimal merece una too11 m: puede identificar un lote de tierra. Es comparable toohello precisión típica de una unidad GPS no corregida y sin interferencias.
* Hola quinto decimal inferior es que vale la pena hasta too1.1 m: que árboles distinguen entre sí. Nivel de precisión toothis con unidades GPS comerciales solo se puede lograr con corrección diferencial.
* posición decimal de la sexta Hola merece la pena seguridad m: too0.11 que ya puede utilizarla para diseñar estructuras en detalle, para diseñar los entornos, crear carreteras. Debería ser más que suficiente para realizar el seguimiento de los movimientos de glaciares y ríos. Esto se consigue al tomar medidas meticulosas con GPS, como GPS corregido de forma diferencial.

información de ubicación de Hello puede ser caracterizará como sigue, separar los región, la ubicación y la información de la ciudad. Tenga en cuenta que también puede llamar a un extremo REST, como la API de Bing Maps disponibles en [buscar una ubicación de punto de](https://msdn.microsoft.com/library/ff701710.aspx) información de tooget Hola región/distrito.

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

Estas características basadas en la ubicación pueden ser más características de recuento adicionales toogenerate usado como se describió anteriormente. 

> [!TIP]
> Puede insertar mediante programación los registros de hello mediante el lenguaje seleccionado. Puede que necesite tooinsert datos de hello en la eficacia de escritura de fragmentos tooimprove (para obtener un ejemplo de cómo toodo este uso pyodbc, consulte [tooaccess de ejemplo HelloWorld A SQL Server con python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)). Otra alternativa es tooinsert base de datos de hello mediante hello [utilidad BCP](https://msdn.microsoft.com/library/ms162802.aspx).
> 
> 

### <a name="sql-aml"></a>Conexión tooAzure aprendizaje automático
característica Hola recién generado puede agrega como una tabla existente de columna tooan o almacenado en una tabla nueva y estar combinada con la tabla original de hello para el aprendizaje automático. Características se pueden genera o acceder si ya ha creado, con hello [importar datos] [ import-data] módulo aprendizaje automático de Azure tal y como se muestra a continuación:

![Lectores de azureml][1] 

## <a name="python"></a>Uso de un lenguaje de programación como Python
Usar datos de Python tooexplore y generar características cuando hello datos están en SQL Server es datos tooprocessing similares en Azure blob mediante Python como se documenta en [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md). datos de Hello toobe cargado desde la base de datos de hello en una trama de datos pandas es necesario y, a continuación, pueden seguir procesándose. Se documente proceso de Hola de conexión de base de datos de toohello y carga datos de hello en la trama de datos de hello en esta sección.

Hola siguiendo el formato de cadena de conexión puede ser usado tooconnect base de datos de SQL Server de la tooa de Python mediante pyodbc (replace servername, dbname, nombre de usuario y contraseña con los valores específicos):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hola [biblioteca Pandas](http://pandas.pydata.org/) en Python proporciona un amplio conjunto de estructuras de datos y herramientas de análisis de datos para la manipulación de datos para la programación de Python. código de Hello siguiente lee devuelven resultados de Hola de una base de datos de SQL Server en una trama de datos de Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Ahora puede trabajar con la trama de datos de hello Pandas tal como se explicó en el artículo hello [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).

## <a name="azure-data-science-in-action-example"></a>Ejemplo de ciencia de datos de Azure en acción
Para obtener un ejemplo de tutorial de extremo a extremo de hello proceso de ciencia de datos de Azure con un conjunto de datos pública, consulte [proceso de ciencia de datos de Azure en acción](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

