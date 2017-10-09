---
title: "aaaExtend U-SQL scripts con Python en análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorun Python código de secuencias de comandos SQL U"
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
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="6438a-103">Tutorial: Introducción a la extensión de U-SQL con Python</span><span class="sxs-lookup"><span data-stu-id="6438a-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="6438a-104">Las extensiones de Python para SQL U permiten a los desarrolladores tooperform masivamente la ejecución en paralelo de código Python.</span><span class="sxs-lookup"><span data-stu-id="6438a-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="6438a-105">Hola siguiente ejemplo muestra los pasos básicos de hello:</span><span class="sxs-lookup"><span data-stu-id="6438a-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="6438a-106">Hola de uso `REFERENCE ASSEMBLY` las extensiones de instrucción tooenable Python para hello Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="6438a-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="6438a-107">Con hello `REDUCE` Hola de operación toopartition los datos en una clave de entrada</span><span class="sxs-lookup"><span data-stu-id="6438a-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="6438a-108">las extensiones de Python para SQL U Hello incluyen un reductor integrado (`Extension.Python.Reducer`) que ejecuta código de Python en cada reductor de toohello vértices asignado</span><span class="sxs-lookup"><span data-stu-id="6438a-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="6438a-109">Hola script U-SQL contiene código Python de hello incrustada que tiene una función denominada `usqlml_main` que acepta un pandas trama de datos como entrada y devuelve una trama de datos como resultado de pandas.</span><span class="sxs-lookup"><span data-stu-id="6438a-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

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
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="6438a-110">¿Cómo se integra Python con U-SQL?</span><span class="sxs-lookup"><span data-stu-id="6438a-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="6438a-111">Tipos de datos</span><span class="sxs-lookup"><span data-stu-id="6438a-111">Datatypes</span></span>

* <span data-ttu-id="6438a-112">Columnas numéricas y de cadena de U-SQL convertidas tal cual entre pandas y U-SQL</span><span class="sxs-lookup"><span data-stu-id="6438a-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="6438a-113">Valores NULL de SQL U son tooand convertido de Pandas `NA` valores</span><span class="sxs-lookup"><span data-stu-id="6438a-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="6438a-114">Esquemas</span><span class="sxs-lookup"><span data-stu-id="6438a-114">Schemas</span></span>

* <span data-ttu-id="6438a-115">Los vectores de índice en Pandas no son compatibles en U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6438a-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="6438a-116">Todos los marcos de datos de entrada en función de Python de hello siempre tienen un índice numérico de 64 bits comprendido entre 0 y el número de Hola de filas menos 1.</span><span class="sxs-lookup"><span data-stu-id="6438a-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="6438a-117">Los conjuntos de datos de U-SQL no pueden tener nombres de columna duplicados</span><span class="sxs-lookup"><span data-stu-id="6438a-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="6438a-118">Los nombres de columna de conjuntos de datos de U-SQL que no son cadenas.</span><span class="sxs-lookup"><span data-stu-id="6438a-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="6438a-119">Versiones de Python</span><span class="sxs-lookup"><span data-stu-id="6438a-119">Python Versions</span></span>
<span data-ttu-id="6438a-120">Se admite solo Python 3.5.1 (compilado para Windows).</span><span class="sxs-lookup"><span data-stu-id="6438a-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="6438a-121">Módulos estándar de Python</span><span class="sxs-lookup"><span data-stu-id="6438a-121">Standard Python modules</span></span>
<span data-ttu-id="6438a-122">Se incluyen todos los módulos de Python estándares de Hola.</span><span class="sxs-lookup"><span data-stu-id="6438a-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="6438a-123">Módulos adicionales de Python</span><span class="sxs-lookup"><span data-stu-id="6438a-123">Additional Python modules</span></span>
<span data-ttu-id="6438a-124">Además de hello bibliotecas estándar de Python, varias bibliotecas de python utilizadas se incluyen:</span><span class="sxs-lookup"><span data-stu-id="6438a-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="6438a-125">Mensajes de excepción</span><span class="sxs-lookup"><span data-stu-id="6438a-125">Exception Messages</span></span>
<span data-ttu-id="6438a-126">Actualmente, se muestra una excepción en el código de Python como un error genérico de vértices.</span><span class="sxs-lookup"><span data-stu-id="6438a-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="6438a-127">Hola futuras, mensajes de error de trabajo de U-SQL de Hola mostrará mensaje de excepción de Python de saludo.</span><span class="sxs-lookup"><span data-stu-id="6438a-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="6438a-128">Limitaciones de tamaño de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="6438a-128">Input and Output size limitations</span></span>
<span data-ttu-id="6438a-129">Cada vértice tiene una cantidad limitada de memoria asignada tooit.</span><span class="sxs-lookup"><span data-stu-id="6438a-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="6438a-130">Actualmente, ese límite es de 6 GB para AU.</span><span class="sxs-lookup"><span data-stu-id="6438a-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="6438a-131">Porque hello deben existir tramas de datos de entrada y salida en la memoria en el código Python de hello, tamaño total del Hola Hola entrada y salida no puede superar los 6 GB.</span><span class="sxs-lookup"><span data-stu-id="6438a-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="6438a-132">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6438a-132">See also</span></span>
* [<span data-ttu-id="6438a-133">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="6438a-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6438a-134">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6438a-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="6438a-135">Uso de funciones de ventana de U-SQL para trabajos de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="6438a-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

