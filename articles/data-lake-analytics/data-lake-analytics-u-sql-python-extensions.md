---
title: "Extensión de los scripts de U-SQL con Python en Azure Data Lake Analytics | Microsoft Docs"
description: "Obtenga información acerca de cómo ejecutar código de Python en scripts de U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d18ef1f747aee2fa01cef9891432d0461031ee4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="ddf0b-103">Tutorial: Introducción a la extensión de U-SQL con Python</span><span class="sxs-lookup"><span data-stu-id="ddf0b-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="ddf0b-104">Las extensiones de Python para U-SQL permiten a los desarrolladores realizar la ejecución en paralelo de forma masiva de código Python.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span></span> <span data-ttu-id="ddf0b-105">En el ejemplo siguiente se muestran los pasos básicos:</span><span class="sxs-lookup"><span data-stu-id="ddf0b-105">The following example illustrates the basic steps:</span></span>

* <span data-ttu-id="ddf0b-106">Uso de la instrucción `REFERENCE ASSEMBLY` para habilitar las extensiones de Python para el script de U-SQL</span><span class="sxs-lookup"><span data-stu-id="ddf0b-106">Use the `REFERENCE ASSEMBLY` statement to enable Python extensions for the U-SQL Script</span></span>
* <span data-ttu-id="ddf0b-107">Uso de la operación `REDUCE` para la partición de datos de entrada de una clave</span><span class="sxs-lookup"><span data-stu-id="ddf0b-107">Using the `REDUCE` operation to partition the input data on a key</span></span>
* <span data-ttu-id="ddf0b-108">Las extensiones de Python para U-SQL incluyen un reductor integrado (`Extension.Python.Reducer`) que ejecuta código de Python en cada vértice asignado al reductor</span><span class="sxs-lookup"><span data-stu-id="ddf0b-108">The Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned to the reducer</span></span>
* <span data-ttu-id="ddf0b-109">El script de U-SQL contiene el código de Python insertado que tiene una función denominada `usqlml_main` que acepta un DataFrame de Pandas como entrada y devuelve un DataFrame de Pandas como salida.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-109">The U-SQL script contains the embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="ddf0b-110">¿Cómo se integra Python con U-SQL?</span><span class="sxs-lookup"><span data-stu-id="ddf0b-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="ddf0b-111">Tipos de datos</span><span class="sxs-lookup"><span data-stu-id="ddf0b-111">Datatypes</span></span>

* <span data-ttu-id="ddf0b-112">Columnas numéricas y de cadena de U-SQL convertidas tal cual entre pandas y U-SQL</span><span class="sxs-lookup"><span data-stu-id="ddf0b-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="ddf0b-113">Los valores Null de U-SQL se conviernten a valores `NA` de Pandas y viceversa</span><span class="sxs-lookup"><span data-stu-id="ddf0b-113">U-SQL Nulls are converted to and from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="ddf0b-114">Esquemas</span><span class="sxs-lookup"><span data-stu-id="ddf0b-114">Schemas</span></span>

* <span data-ttu-id="ddf0b-115">Los vectores de índice en Pandas no son compatibles en U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="ddf0b-116">Todas las tramas de datos de entrada en la función Python siempre tienen un índice numérico de 64 bits comprendido entre 0 y el número de filas menos 1.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span></span> 
* <span data-ttu-id="ddf0b-117">Los conjuntos de datos de U-SQL no pueden tener nombres de columna duplicados</span><span class="sxs-lookup"><span data-stu-id="ddf0b-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="ddf0b-118">Los nombres de columna de conjuntos de datos de U-SQL que no son cadenas.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="ddf0b-119">Versiones de Python</span><span class="sxs-lookup"><span data-stu-id="ddf0b-119">Python Versions</span></span>
<span data-ttu-id="ddf0b-120">Se admite solo Python 3.5.1 (compilado para Windows).</span><span class="sxs-lookup"><span data-stu-id="ddf0b-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="ddf0b-121">Módulos estándar de Python</span><span class="sxs-lookup"><span data-stu-id="ddf0b-121">Standard Python modules</span></span>
<span data-ttu-id="ddf0b-122">Se incluyen todos los módulos estándar de Python.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-122">All the standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="ddf0b-123">Módulos adicionales de Python</span><span class="sxs-lookup"><span data-stu-id="ddf0b-123">Additional Python modules</span></span>
<span data-ttu-id="ddf0b-124">Además de las bibliotecas estándar de Python, se incluyen varias bibliotecas de python de uso frecuente:</span><span class="sxs-lookup"><span data-stu-id="ddf0b-124">Besides the standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="ddf0b-125">Mensajes de excepción</span><span class="sxs-lookup"><span data-stu-id="ddf0b-125">Exception Messages</span></span>
<span data-ttu-id="ddf0b-126">Actualmente, se muestra una excepción en el código de Python como un error genérico de vértices.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="ddf0b-127">En el futuro, los mensajes de error de trabajo de U-SQL mostrarán el mensaje de excepción de Python.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-127">In the future, the U-SQL Job error messages will display the Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="ddf0b-128">Limitaciones de tamaño de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="ddf0b-128">Input and Output size limitations</span></span>
<span data-ttu-id="ddf0b-129">Cada vértice tiene una cantidad limitada de memoria asignada a él.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-129">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="ddf0b-130">Actualmente, ese límite es de 6 GB para AU.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="ddf0b-131">Dado que las DataFrames de entrada y salida deben existir en la memoria en el código de Python, el tamaño total de la entrada y salida no puede superar los 6 GB.</span><span class="sxs-lookup"><span data-stu-id="ddf0b-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="ddf0b-132">Consulte también</span><span class="sxs-lookup"><span data-stu-id="ddf0b-132">See also</span></span>
* [<span data-ttu-id="ddf0b-133">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ddf0b-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="ddf0b-134">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ddf0b-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="ddf0b-135">Uso de funciones de ventana de U-SQL para trabajos de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ddf0b-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

