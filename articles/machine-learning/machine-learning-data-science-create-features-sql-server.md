---
title: "características de aaaCreate para datos de SQL Server utilizando SQL y Python | Documentos de Microsoft"
description: Procesar datos de SQL Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a>Creación de características para datos de SQL Server con SQL y Python
Este documento muestra cómo toogenerate características de los datos almacenados en una VM de SQL Server en Azure que le ayudan a algoritmos aprender más eficazmente datos Hola. Esto puede hacerse con SQL o con un lenguaje de programación como Python; las dos opciones se muestran aquí.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Esto **menú** vincula tootopics que describen cómo toocreate características para los datos en varios entornos. Esta tarea es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

> [!NOTE]
> Para obtener un ejemplo práctico, puede consultar hello [conjunto de datos de Nueva York Taxi](http://www.andresmh.com/nyctaxitrips/) y consulte toohello IPNB titulada [datos NYC problemas con mediante el Bloc de notas de IPython y SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para un tutorial to-end.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que ha:

* Creado una cuenta de almacenamiento de Azure. Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Almacenado los datos en SQL Server. Si no fue así, consulte [mover datos tooan base de datos de SQL Azure para el aprendizaje automático de Azure](machine-learning-data-science-move-sql-azure.md) para obtener instrucciones sobre cómo toomove Hola datos en él.

## <a name="sql-featuregen"></a>Generación de características con SQL
En esta sección, se describen formas de generar características mediante SQL:  

1. [Generación de características basadas en recuentos](#sql-countfeature)
2. [Generación de características de discretización](#sql-binningfeature)
3. [Implementar características de Hola de una sola columna](#sql-featurerollout)

> [!NOTE]
> Una vez que generar características adicionales, puede agregarlas como tabla de columnas toohello existente o crear una nueva tabla con características adicionales de Hola y la clave principal, que puede combinarse con la tabla original de Hola.
> 
> 

### <a name="sql-countfeature"></a>Generación de características basadas en recuentos
En este documento se muestran dos maneras de generar características de recuento. Hola primero usa suma condicional y el segundo método utiliza de Hola Hola cláusula 'where'. Estos, a continuación, pueden combinarse con hello original (con columnas de clave principal) toohave recuento características para tablas junto con los datos originales de Hola.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a>Generación de características de discretización
Hello en el ejemplo siguiente se muestra cómo toogenerate había discretizado características mediante discretización (utiliza 5 bins) una columna numérica que puede utilizarse como una característica en su lugar:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Implementar características de Hola de una sola columna
En esta sección, demostraremos cómo tooroll horizontal una sola columna en una tabla toogenerate más características. ejemplo de Hola se da por supuesto que hay una columna de latitud o longitud de tabla Hola desde el que está tratando de toogenerate características.

Aquí se incluye un breve manual sobre los datos de ubicación de latitud y longitud (extraído de stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`). Esto es útil toounderstand antes de campo de ubicación de hello featurizing:

* inicio de sesión de Hello nos dice si estamos Norte o sur, este u oeste mundo Hola.
* Un dígito de las centenas distinto de cero indica que se usa la longitud y no la latitud.
* dígito de Hello decenas ofrece un tooabout posición 1.000 kilómetros. Nos brinda información útil sobre el continente u océano en el que nos encontramos.
* dígito de unidades de Hello (un grado decimal) ofrece una posición hacia arriba too111 kilómetros (60 millas náuticas, unos 69 millas). Puede informarnos aproximadamente del estado grande o país en que nos encontramos.
* Hola primer decimal merece una too11.1 km: puede distinguir la posición de Hola de una ciudad grande de una ciudad grande vecino.
* Hola segundo decimal merece una too1.1 km: puede separar un pueblo de Hola a continuación.
* posición decimal de la tercera Hola merece la pena seguridad too110 m: puede identificar un campo agrícola grande o recinto institucional.
* Hola cuarto decimal merece una too11 m: puede identificar un lote de tierra. Es comparable toohello precisión típica de una unidad GPS no corregida y sin interferencias.
* Hello quinto decimal inferior es que vale la pena seguridad too1.1 m: distinguir árboles entre sí. Nivel de precisión toothis con unidades GPS comerciales solo se puede lograr con corrección diferencial.
* posición decimal de la sexta Hola merece la pena seguridad m: too0.11 que ya puede utilizarla para diseñar estructuras en detalle, para diseñar los entornos, crear carreteras. Debería ser más que suficiente para realizar el seguimiento de los movimientos de glaciares y ríos. Esto se consigue al tomar medidas meticulosas con GPS, como GPS corregido de forma diferencial.

información de ubicación de Hello puede puede ser caracterizará como sigue, separar los región, la ubicación y la información de la ciudad. Tenga en cuenta que una vez también puede llamar a un extremo REST, como la API de Bing Maps disponibles en `https://msdn.microsoft.com/library/ff701710.aspx` información de tooget Hola región/distrito.

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

Hola por encima de la ubicación basada en características pueden ser más usa características de recuento adicionales toogenerate como se describió anteriormente.

> [!TIP]
> Puede insertar mediante programación los registros de hello mediante el lenguaje seleccionado. Puede que necesite tooinsert datos de hello en la eficacia de escritura de fragmentos tooimprove [extraer del repositorio en el ejemplo de cómo se hello toodo esta con pyodbc aquí](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).
> Otra alternativa es tooinsert datos en la base de datos de hello mediante [utilidad BCP](https://msdn.microsoft.com/library/ms162802.aspx)
> 
> 

### <a name="sql-aml"></a>Conexión tooAzure aprendizaje automático
característica Hola recién generado puede agrega como una tabla existente de columna tooan o almacenado en una tabla nueva y estar combinada con la tabla original de hello para el aprendizaje automático. Características se pueden genera o acceder si ya ha creado, con hello [importar datos](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) módulo en aprendizaje automático de Azure, tal y como se muestra a continuación:

![Lectores de azureml](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a>Uso de un lenguaje de programación como Python
Utilizar funciones de toogenerate de Python cuando Hola datos en SQL Server es datos tooprocessing similares en Azure blob mediante Python como se documenta en [datos de Blob de Azure de proceso en entorno ciencia de datos](machine-learning-data-science-process-data-blob.md). datos de Hello toobe cargado desde la base de datos de hello en una trama de datos pandas es necesario y, a continuación, pueden seguir procesándose. Se documente proceso de Hola de conexión de base de datos de toohello y carga datos de hello en la trama de datos de hello en esta sección.

Hola siguiendo el formato de cadena de conexión puede ser usado tooconnect base de datos de SQL Server de la tooa de Python mediante pyodbc (replace servername, dbname, nombre de usuario y contraseña con los valores específicos):

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hola [biblioteca Pandas](http://pandas.pydata.org/) en Python proporciona un amplio conjunto de estructuras de datos y herramientas de análisis de datos para la manipulación de datos para la programación de Python. código de Hello siguiente lee devuelven resultados de Hola de una base de datos de SQL Server en una trama de datos de Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Ahora puede trabajar con la trama de datos de hello Pandas tal como se explicó en temas [crear características de datos de almacenamiento de blobs de Azure utilizando Panda](machine-learning-data-science-create-features-blob.md).

