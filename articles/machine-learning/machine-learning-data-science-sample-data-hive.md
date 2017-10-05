---
title: Muestreo de datos en tablas de HDInsight Hive de Azure | Microsoft Docs
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
ms.openlocfilehash: d46297dfaf85976114fbf610803e5f1a997041e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Muestreo de datos en tablas de HDInsight Hive de Azure
En este artículo, se describe cómo reducir la muestra de datos almacenados en tablas de HDInsight Hive de Azure mediante consultas de Hive. Se explican tres métodos de muestreo normalmente utilizados:

* Muestreo aleatorio uniforme
* Muestreo aleatorio por grupos
* Muestreo estratificado

El siguiente **menú** está vinculado a temas que describen cómo realizar un muestreo de datos desde varios entornos de almacenamiento.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**¿Por qué realizar un muestreo de los datos?**
Si el conjunto de datos que pretende analizar es grande, es recomendable reducirlo a un tamaño más pequeño, pero representativo, que sea más manejable. Esto facilita la comprensión y exploración de los datos, y el diseño de características. Su rol en el proceso de ciencia de datos en equipos es permitir la rápida creación de prototipos de las funciones de procesamiento de datos y de los modelos de aprendizaje automático.

Esta tarea de muestreo es un paso en el [proceso de ciencia de datos en equipos (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-to-submit-hive-queries"></a>Cómo enviar consultas de Hive
Las consultas de subárbol se pueden enviar desde la consola de línea de comandos de Hadoop del nodo principal del clúster de Hadoop. Para ello, inicie sesión en el nodo principal del clúster de Hadoop, abra la consola de la línea de comandos de Hadoop y envíe las consultas de Hive desde allí. Para obtener instrucciones sobre el envío de consultas de Hive en la consola de línea de comandos de Hadoop, consulte [Envío de consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a> Muestra aleatoria uniforme
El muestreo aleatorio uniforme implica que cada fila del conjunto de datos tiene la misma probabilidad de muestreo. Esto se puede implementar añadiendo un campo adicional de rand() al conjunto de datos en la consulta "select" interna, y en la consulta "select" externa esa condición en ese campo aleatorio.

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

En este caso, `<sample rate, 0-1>` especifica la proporción de registros que los usuarios quieren usar como muestra.

## <a name="group"></a> Muestreo aleatorio por grupos
Cuando se realiza un muestreo de datos de categoría, podría querer incluir o excluir todas las instancias de algún valor concreto de una variable de categoría. Esto es lo que significa "muestreo por grupos".
Por ejemplo, si tiene una variable de categoría "Estado", que tiene como valores NY, MA, CA, NJ, PA, etc., querrá que los registros de un mismo estado estén siempre juntos, ya están muestreados o no.

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
El muestreo aleatorio se estratifica con respecto a una variable de categoría cuando las muestras obtenidas tienen valores de esa categoría que se encuentran en la misma proporción que en la población original de la que se obtuvieron las muestras. En el mismo ejemplo que el anterior, suponga que los datos tienen subpoblaciones según los estados; por ejemplo, NJ tiene 100 observaciones, NY tiene 60 observaciones y WA tiene 300 observaciones. Si especifica que la tasa de muestreo estratificado sea 0,5, la muestra obtenida debería tener aproximadamente 50, 30 y 150 observaciones de NJ, NY y WA, respectivamente.

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

