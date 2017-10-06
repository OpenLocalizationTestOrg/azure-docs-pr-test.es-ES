---
title: "aaaExplore datos en máquina de Virtual de SQL Server en Azure | Documentos de Microsoft"
description: "¿Cómo tooexplore datos que se almacenan en una VM de SQL Server en Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Exploración de los datos de una máquina virtual de SQL Server en Azure
Este documento cubre cómo tooexplore datos que se almacenan en una VM de SQL Server en Azure. Esto puede hacerse mediante la administración de datos usando SQL o mediante un lenguaje de programación como Python.

siguiente Hello **menú** vincula tootopics que describen cómo toouse herramientas tooexplore datos desde varios entornos de almacenamiento. Esta tarea es un paso en el proceso de análisis de Cortana (CAP) Hola.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> instrucciones de SQL de ejemplo de Hola en este documento se suponen que los datos están en SQL Server. Si no es así, consulte cómo toohello nube datos ciencia proceso mapa toolearn toomove su tooSQL de datos servidor.
> 
> 

## <a name="sql-dataexploration"></a>Exploración de los datos de SQL con scripts de SQL
Estos son algunos scripts SQL de ejemplo que pueden ser utilizados tooexplore almacenes de datos en SQL Server.

1. Obtener el recuento de Hola de observaciones por día
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Obtener niveles de hello en una columna de categorías
   
    `select  distinct <column_name> from <databasename>`
3. Obtener número de Hola de niveles de combinación de dos columnas de categorías 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Obtener la distribución de Hola para columnas numéricas
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Para obtener un ejemplo práctico, puede usar hello [conjunto de datos de Nueva York Taxi](http://www.andresmh.com/nyctaxitrips/) y consulte toohello IPNB titulada [datos NYC problemas con mediante el Bloc de notas de IPython y SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para un tutorial to-end.
> 
> 

## <a name="python"></a>Exploración de los datos de SQL con Python
Usar datos de Python tooexplore y generar características cuando hello datos están en SQL Server es datos tooprocessing similares en Azure blob mediante Python, tal como se documenta en [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md). datos de Hello toobe cargado desde la base de datos de hello en una trama de datos de pandas es necesario y, a continuación, pueden seguir procesándose. Se documente proceso Hola de conexión de base de datos de toohello y cargar datos de hello en hello trama de datos de esta sección.

Hola siguiendo el formato de cadena de conexión puede ser usado tooconnect base de datos de SQL Server de la tooa de Python mediante pyodbc (replace servername, dbname, nombre de usuario y contraseña con los valores específicos):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hola [biblioteca Pandas](http://pandas.pydata.org/) en Python proporciona un amplio conjunto de estructuras de datos y herramientas de análisis de datos para la manipulación de datos para la programación de Python. Hello siguiente código lee devuelven resultados de Hola de una base de datos de SQL Server en una trama de datos de Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Ahora puede trabajar con hello Pandas trama de datos tal como se explicó en el tema de hello [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Ejemplo de proceso de análisis de Cortana en acción
Para obtener un ejemplo de tutorial de extremo a extremo de hello proceso de análisis de Cortana con un conjunto de datos público, consulte [Hola proceso de ciencia de datos de equipo en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

