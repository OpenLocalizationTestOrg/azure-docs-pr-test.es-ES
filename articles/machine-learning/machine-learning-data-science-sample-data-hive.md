---
title: aaaSample datos en tablas de HDInsight Hive de Azure | Documentos de Microsoft
description: "Reducción del muestreo de datos en tablas de HDInsight Hive (Hadopop) de Azure"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Muestreo de datos en tablas de HDInsight Hive de Azure
En este artículo, se describen los datos de ejemplo de toodown cómo almacenados en tablas de HDInsight Hive de Azure usan consultas de Hive. Se explican tres métodos de muestreo normalmente utilizados:

* Muestreo aleatorio uniforme
* Muestreo aleatorio por grupos
* Muestreo estratificado

siguiente Hello **menú** vincula tootopics que describen cómo toosample datos desde varios entornos de almacenamiento.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**¿Por qué realizar un muestreo de los datos?**
Si piensa tooanalyze de conjunto de datos de hello es grande, normalmente es un tooreduce de datos de ejemplo toodown Hola buena idea tooa más pequeño pero representativo y más fáciles de administrar el tamaño. Esto facilita la comprensión y exploración de los datos, y el diseño de características. Su función en hello proceso de ciencia de datos de equipo es tooenable la creación de prototipos rápida de las funciones de procesamiento de datos de Hola y modelos de aprendizaje automático.

Esta tarea de muestreo es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>¿Cómo toosubmit consultas de Hive
Las consultas de Hive pueden enviarse desde la consola de línea de comandos de Hadoop de hello en del nodo principal del clúster de Hadoop de Hola Hola. toodo esto, inicie sesión en el nodo principal de Hola de clúster de Hadoop de hello, abra Hola consola de línea de comandos de Hadoop así como enviar consultas de Hive Hola desde allí. Para obtener instrucciones sobre cómo enviar consultas de Hive en la consola de línea de comandos de Hadoop de hello, consulte [cómo tooSubmit consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a> Muestra aleatoria uniforme
Muestreo aleatorio uniforme significa que cada fila de conjunto de datos de hello tiene la misma probabilidad de que se va a muestrear. Esto puede implementarse mediante la adición de un conjunto de datos de campo adicional rand() toohello en la consulta "select" interna de Hola y de Hola externa consulta "select" esa condición en ese campo aleatorio.

Aquí se muestra una consulta de ejemplo:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

En este caso, `<sample rate, 0-1>` especifica la proporción de Hola de registros que desean que los usuarios de hello toosample.

## <a name="group"></a> Muestreo aleatorio por grupos
Cuando los datos de categorías de muestreo, puede que desee tooeither incluir o excluir todas las instancias de Hola de algún valor de una variable de categoría determinado. Esto es lo que significa "muestreo por grupos".
Por ejemplo, si tiene una variable de categoría "Estado", que tiene valores de Nueva York, MA, CA, NJ, PA, etcetera, desea que los registros de hello mismo estado ser siempre juntos, si están muestreadas o no.

Aquí se muestra una consulta de ejemplo que realiza un muestreo por grupo:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Muestreo estratificado
Muestreo aleatorio es estratificado con sentido tooa variable de categoría cuando las muestras Hola obtenidas tienen valores de categorías es que se encuentran en hello misma relación como en la población de hello primario desde qué Hola se obtuvieron los ejemplos. Uso de Hola mismo ejemplo anterior, supongamos que los datos tienen subcarpetas rellenados por los Estados, digamos NJ tiene 100 observaciones, NY tiene 60 observaciones y WA tiene 300 observaciones. Si se especifica la velocidad de Hola de estratificado muestreo toobe 0,5, a continuación, hello muestra obtenido debe tener aproximadamente 50, 30 y 150 observaciones de nueva Jersey y Nueva York, WA respectivamente.

Aquí se muestra una consulta de ejemplo:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Para obtener información sobre los métodos de muestreo más avanzados que están disponibles en Hive, consulte [Manual de lenguaje: muestreo](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

