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
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Tutorial: Introducción a la extensión de U-SQL con Python

Las extensiones de Python para SQL U permiten a los desarrolladores tooperform masivamente la ejecución en paralelo de código Python. Hola siguiente ejemplo muestra los pasos básicos de hello:

* Hola de uso `REFERENCE ASSEMBLY` las extensiones de instrucción tooenable Python para hello Script U-SQL
* Con hello `REDUCE` Hola de operación toopartition los datos en una clave de entrada
* las extensiones de Python para SQL U Hello incluyen un reductor integrado (`Extension.Python.Reducer`) que ejecuta código de Python en cada reductor de toohello vértices asignado
* Hola script U-SQL contiene código Python de hello incrustada que tiene una función denominada `usqlml_main` que acepta un pandas trama de datos como entrada y devuelve una trama de datos como resultado de pandas.

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

## <a name="how-python-integrates-with-u-sql"></a>¿Cómo se integra Python con U-SQL?

### <a name="datatypes"></a>Tipos de datos

* Columnas numéricas y de cadena de U-SQL convertidas tal cual entre pandas y U-SQL
* Valores NULL de SQL U son tooand convertido de Pandas `NA` valores

### <a name="schemas"></a>Esquemas

* Los vectores de índice en Pandas no son compatibles en U-SQL. Todos los marcos de datos de entrada en función de Python de hello siempre tienen un índice numérico de 64 bits comprendido entre 0 y el número de Hola de filas menos 1. 
* Los conjuntos de datos de U-SQL no pueden tener nombres de columna duplicados
* Los nombres de columna de conjuntos de datos de U-SQL que no son cadenas. 

### <a name="python-versions"></a>Versiones de Python
Se admite solo Python 3.5.1 (compilado para Windows). 

### <a name="standard-python-modules"></a>Módulos estándar de Python
Se incluyen todos los módulos de Python estándares de Hola.

### <a name="additional-python-modules"></a>Módulos adicionales de Python
Además de hello bibliotecas estándar de Python, varias bibliotecas de python utilizadas se incluyen:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Mensajes de excepción
Actualmente, se muestra una excepción en el código de Python como un error genérico de vértices. Hola futuras, mensajes de error de trabajo de U-SQL de Hola mostrará mensaje de excepción de Python de saludo.

### <a name="input-and-output-size-limitations"></a>Limitaciones de tamaño de entrada y salida
Cada vértice tiene una cantidad limitada de memoria asignada tooit. Actualmente, ese límite es de 6 GB para AU. Porque hello deben existir tramas de datos de entrada y salida en la memoria en el código Python de hello, tamaño total del Hola Hola entrada y salida no puede superar los 6 GB.

## <a name="see-also"></a>Otras referencias
* [Información general de Análisis de Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Uso de funciones de ventana de U-SQL para trabajos de Análisis de Azure Data Lake](data-lake-analytics-use-window-functions.md)

