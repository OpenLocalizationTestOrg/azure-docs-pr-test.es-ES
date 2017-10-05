---
title: "Exploración de los datos de una máquina virtual de SQL Server en Azure | Microsoft Docs"
description: "Cómo explorar los datos que se almacenan en una máquina virtual de SQL Server en Azure."
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
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="9d93a-103">Exploración de los datos de una máquina virtual de SQL Server en Azure</span><span class="sxs-lookup"><span data-stu-id="9d93a-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="9d93a-104">Este documento explica cómo explorar los datos que se almacenan en una máquina virtual de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="9d93a-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="9d93a-105">Esto puede hacerse mediante la administración de datos usando SQL o mediante un lenguaje de programación como Python.</span><span class="sxs-lookup"><span data-stu-id="9d93a-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="9d93a-106">El siguiente **menú** vincula a temas que describen cómo usar herramientas para explorar los datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9d93a-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="9d93a-107">Esta tarea es un paso en el proceso de análisis de Cortana (CAP).</span><span class="sxs-lookup"><span data-stu-id="9d93a-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="9d93a-108">En las instrucciones SQL de ejemplo de este documento se supone que los datos están en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9d93a-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="9d93a-109">Si no lo están, consulte el mapa de proceso de ciencia de datos en la nube para obtener información sobre cómo mover los datos a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9d93a-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="9d93a-110"><a name="sql-dataexploration"></a>Exploración de los datos de SQL con scripts de SQL</span><span class="sxs-lookup"><span data-stu-id="9d93a-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="9d93a-111">A continuación se muestran algunos scripts de SQL de ejemplo que se pueden usar para explorar los almacenes de datos en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9d93a-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="9d93a-112">Obtener el número de observaciones por día</span><span class="sxs-lookup"><span data-stu-id="9d93a-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="9d93a-113">Obtenga los niveles de una columna de categorías</span><span class="sxs-lookup"><span data-stu-id="9d93a-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="9d93a-114">Obtener el número de niveles de combinación de dos columnas de categorías</span><span class="sxs-lookup"><span data-stu-id="9d93a-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="9d93a-115">Obtención de la distribución para columnas numéricas </span><span class="sxs-lookup"><span data-stu-id="9d93a-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="9d93a-116">Para obtener un ejemplo práctico, puede usar el [conjunto de datos de los taxis de la Ciudad de Nueva York](http://www.andresmh.com/nyctaxitrips/) y consultar el IPNB llamado [Tratamiento de datos de la Ciudad de Nueva York mediante un Bloc de notas de IPython y SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb), que se trata de un tutorial completo.</span><span class="sxs-lookup"><span data-stu-id="9d93a-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="9d93a-117"><a name="python"></a>Exploración de los datos de SQL con Python</span><span class="sxs-lookup"><span data-stu-id="9d93a-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="9d93a-118">Usar Python para generar explorar datos y generar características cuando los datos están en SQL Server es parecido a procesar los datos en Blob de Azure mediante Python, como se documenta en [Proceso de datos de Blob de Azure en su entorno de ciencia de datos](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9d93a-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="9d93a-119">Los datos deben cargarse desde la base de datos en una trama de datos de Pandas y, a continuación, se pueden procesar aún más.</span><span class="sxs-lookup"><span data-stu-id="9d93a-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="9d93a-120">Se documenta el proceso de conexión a la base de datos y carga de los datos en la trama de datos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="9d93a-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="9d93a-121">El formato de cadena de conexión siguiente puede usarse para conectarse a una base de datos de SQL Server desde Python mediante pyodbc (reemplace servername, dbname, username y password con sus valores específicos):</span><span class="sxs-lookup"><span data-stu-id="9d93a-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="9d93a-122">La [biblioteca Pandas](http://pandas.pydata.org/) en Python ofrece un amplio conjunto de herramientas de análisis de datos y estructuras de datos para la manipulación de datos para la programación en Python.</span><span class="sxs-lookup"><span data-stu-id="9d93a-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="9d93a-123">El código siguiente lee los resultados que se devuelven desde una base de datos de SQL Server en una trama de datos de Pandas:</span><span class="sxs-lookup"><span data-stu-id="9d93a-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="9d93a-124">Ya puede trabajar con la trama de datos de Pandas como se explica en el artículo [Proceso de datos del blob de Azure con análisis avanzado](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9d93a-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="9d93a-125">Ejemplo de proceso de análisis de Cortana en acción</span><span class="sxs-lookup"><span data-stu-id="9d93a-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="9d93a-126">Para ver un tutorial de ejemplo completo del proceso de Cortana Analytics usando un conjunto de datos público, consulte [Proceso de ciencia de datos en equipos en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9d93a-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

