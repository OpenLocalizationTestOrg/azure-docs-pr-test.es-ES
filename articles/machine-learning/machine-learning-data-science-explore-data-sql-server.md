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
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="9a8ac-103">Exploración de los datos de una máquina virtual de SQL Server en Azure</span><span class="sxs-lookup"><span data-stu-id="9a8ac-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="9a8ac-104">Este documento cubre cómo tooexplore datos que se almacenan en una VM de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="9a8ac-105">Esto puede hacerse mediante la administración de datos usando SQL o mediante un lenguaje de programación como Python.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="9a8ac-106">siguiente Hello **menú** vincula tootopics que describen cómo toouse herramientas tooexplore datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="9a8ac-107">Esta tarea es un paso en el proceso de análisis de Cortana (CAP) Hola.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="9a8ac-108">instrucciones de SQL de ejemplo de Hola en este documento se suponen que los datos están en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="9a8ac-109">Si no es así, consulte cómo toohello nube datos ciencia proceso mapa toolearn toomove su tooSQL de datos servidor.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="9a8ac-110"><a name="sql-dataexploration"></a>Exploración de los datos de SQL con scripts de SQL</span><span class="sxs-lookup"><span data-stu-id="9a8ac-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="9a8ac-111">Estos son algunos scripts SQL de ejemplo que pueden ser utilizados tooexplore almacenes de datos en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="9a8ac-112">Obtener el recuento de Hola de observaciones por día</span><span class="sxs-lookup"><span data-stu-id="9a8ac-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="9a8ac-113">Obtener niveles de hello en una columna de categorías</span><span class="sxs-lookup"><span data-stu-id="9a8ac-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="9a8ac-114">Obtener número de Hola de niveles de combinación de dos columnas de categorías</span><span class="sxs-lookup"><span data-stu-id="9a8ac-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="9a8ac-115">Obtener la distribución de Hola para columnas numéricas</span><span class="sxs-lookup"><span data-stu-id="9a8ac-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="9a8ac-116">Para obtener un ejemplo práctico, puede usar hello [conjunto de datos de Nueva York Taxi](http://www.andresmh.com/nyctaxitrips/) y consulte toohello IPNB titulada [datos NYC problemas con mediante el Bloc de notas de IPython y SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para un tutorial to-end.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="9a8ac-117"><a name="python"></a>Exploración de los datos de SQL con Python</span><span class="sxs-lookup"><span data-stu-id="9a8ac-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="9a8ac-118">Usar datos de Python tooexplore y generar características cuando hello datos están en SQL Server es datos tooprocessing similares en Azure blob mediante Python, tal como se documenta en [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9a8ac-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="9a8ac-119">datos de Hello toobe cargado desde la base de datos de hello en una trama de datos de pandas es necesario y, a continuación, pueden seguir procesándose.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="9a8ac-120">Se documente proceso Hola de conexión de base de datos de toohello y cargar datos de hello en hello trama de datos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="9a8ac-121">Hola siguiendo el formato de cadena de conexión puede ser usado tooconnect base de datos de SQL Server de la tooa de Python mediante pyodbc (replace servername, dbname, nombre de usuario y contraseña con los valores específicos):</span><span class="sxs-lookup"><span data-stu-id="9a8ac-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="9a8ac-122">Hola [biblioteca Pandas](http://pandas.pydata.org/) en Python proporciona un amplio conjunto de estructuras de datos y herramientas de análisis de datos para la manipulación de datos para la programación de Python.</span><span class="sxs-lookup"><span data-stu-id="9a8ac-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="9a8ac-123">Hello siguiente código lee devuelven resultados de Hola de una base de datos de SQL Server en una trama de datos de Pandas:</span><span class="sxs-lookup"><span data-stu-id="9a8ac-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="9a8ac-124">Ahora puede trabajar con hello Pandas trama de datos tal como se explicó en el tema de hello [datos de Blob de Azure de proceso en el entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9a8ac-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="9a8ac-125">Ejemplo de proceso de análisis de Cortana en acción</span><span class="sxs-lookup"><span data-stu-id="9a8ac-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="9a8ac-126">Para obtener un ejemplo de tutorial de extremo a extremo de hello proceso de análisis de Cortana con un conjunto de datos público, consulte [Hola proceso de ciencia de datos de equipo en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9a8ac-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

