---
title: "características de aaaCreate para los datos en un clúster de Hadoop mediante consultas de Hive | Documentos de Microsoft"
description: "Ejemplos de consultas de Hive que generan características en datos almacenados en un clúster de Hadoop de HDInsight de Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Crear características para datos en un clúster de Hadoop mediante consultas de Hive
Este documento muestra cómo toocreate características para los datos almacenan en un clúster de Hadoop de HDInsight de Azure mediante consultas de Hive. Estas consultas de Hive usan incrustado Hive User Defined Functions (UDF), scripts de hello para el que se proporcionan.

Hola operaciones necesarias toocreate características pueden consumir mucha memoria. rendimiento de Hola de consultas de Hive resulta más importante en estos casos y se puede mejorar con determinados parámetros de ajuste. Hello para la optimización de estos parámetros se describe en la sección final Hola.

Ejemplos de consultas de Hola que se presentan son específico toohello [NYC Taxi recorridos datos](http://chriswhong.com/open-data/foil_nyc_taxi/) escenarios también se proporcionan en [repositorio de GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Estas consultas ya tiene el esquema de datos especificado y está listo toobe enviado toorun. En la sección final de hello, también se describen los parámetros que los usuarios pueden ajustar para que se puede mejorar el rendimiento de Hola de consultas de Hive.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Esto **menú** vincula tootopics que describen cómo toocreate características para los datos en varios entornos. Esta tarea es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que ha:

* Creado una cuenta de almacenamiento de Azure. Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Aprovisionar un clúster de Hadoop personalizado con hello servicio HDInsight.  Si necesita instrucciones, consulte [Personalización de clústeres de Hadoop de HDInsight de Azure para análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).
* datos de Hello ha sido cargado tooHive tablas en clústeres de HDInsight Hadoop de Azure. Si no es así, siga [carga y crear tablas de tooHive datos](machine-learning-data-science-move-hive-tables.md) tooupload datos tooHive tablas en primer lugar.
* Clúster de toohello de acceso remoto habilitado. Si necesita instrucciones, consulte [Hola de acceso principal del nodo de clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Generación de características
En esta sección se describen varios ejemplos de formas de hello en el que se pueden generar características usan consultas de Hive. Una vez haya generado características adicionales, puede agregarlas como tabla de columnas toohello existente o crear una nueva tabla con características adicionales de Hola y la clave principal, que, a continuación, puede combinarse con la tabla original de Hola. Estos son ejemplos de hello presentados:

1. [Generación de características basada en frecuencia](#hive-frequencyfeature)
2. [Riesgos de las variables de categorías en la clasificación binaria](#hive-riskfeature)
3. [Extraer características de campos de fecha y hora](#hive-datefeatures)
4. [Extraer características del campo de texto](#hive-textfeatures)
5. [Calcular distancia entre las coordenadas GPS](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Generación de características basada en frecuencia
A menudo resulta útil toocalculate las frecuencias de Hola de hello niveles de una variable de categoría o las frecuencias de Hola de ciertas combinaciones de niveles de varias variables de categorías. Los usuarios pueden usar Hola después de la secuencia de comandos toocalculate estas frecuencias:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Riesgos de las variables de categorías en la clasificación binaria
En la clasificación binaria, necesitamos tooconvert las variables de categorías no numéricos en características numéricas cuando modelos Hola usándola solo tienen características numéricas. Para ello, reemplace cada nivel no numérico por un riesgo numérico. En esta sección, se muestran algunas consultas de Hive genéricos que calculen los valores de riesgo de hello (logaritmos de posibilidades) de una variable de categoría.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

En este ejemplo, las variables `smooth_param1` y `smooth_param2` se calculan valores de riesgo de conjunto toosmooth Hola de datos de Hola. Los riesgos tienen un intervalo comprendido entre -Inf y Inf. Los riesgos > 0 indica que probabilidad de Hola que tienen como destino hello es igual too1 es mayor que 0.5.

Después de que se calcula la tabla de riesgo de hello, los usuarios pueden asignar tooa tabla de valores de riesgos mediante la combinación con la tabla de riesgo de Hola. consulta de unión de Hive Hola se proporcionó en la sección anterior.

### <a name="hive-datefeatures"></a>Extraer características de campos de fecha y hora
El subárbol se incluye con un conjunto de UDF para el procesamiento de campos de fecha y hora. En el subárbol, formato de fecha y hora de hello predeterminado es ' aaaa-MM-dd 00:00:00 ' ('1970-01-01 12:21:32 ' por ejemplo). En esta sección, se muestran ejemplos que extraer Hola día de un mes, el mes de Hola de un campo de fecha y hora y otros ejemplos que convertir una cadena de fecha y hora en un formato de cadena de fecha y hora de tooa de formato de hello predeterminada en el formato predeterminado.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Esta consulta de Hive se da por supuesto que hello *&#60; campo de fecha y hora >* está en formato de fecha y hora de hello predeterminado.

Si no es un campo de fecha y hora en formato predeterminado de hello, necesita campo de fecha y hora de hello tooconvert en la marca de tiempo de Unix en primer lugar y, a continuación, hora de Unix de Hola de convert marca tooa datetime de cadena que se encuentra en valor predeterminado de Hola formato. Una vez Hola fecha y hora de forma predeterminada en formato, los usuarios pueden aplicar Hola incrustado datetime UDF tooextract características.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

En esta consulta, si hello *&#60; campo de fecha y hora >* tiene Hola patrón como *26/03/2015 12:04:39*, hello *' &#60; el patrón del campo de fecha y hora de hello >'* debería ser `'MM/dd/yyyy HH:mm:ss'`. tootest, los usuarios pueden ejecutar

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Hola *hivesampletable* en esta consulta viene preinstalado en todos los clústeres de Hadoop de HDInsight de Azure de forma predeterminada cuando se aprovisionan clústeres Hola.

### <a name="hive-textfeatures"></a>Extracción de características de campos de texto
Cuando la tabla de Hive hello tiene un campo de texto que contiene una cadena de palabras que están delimitados por espacios, hello siguiente consulta extrae longitud Hola de cadena de Hola y número de Hola de palabras en la cadena de Hola.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Cálculo de la distancia entre conjuntos de coordenadas de GPS
consulta de Hello proporcionado en esta sección puede ser toohello directamente aplicado NYC Taxi recorridos datos. Hola de esta consulta sirve tooshow cómo tooapply incrustada funciones matemáticas en las características de toogenerate de Hive.

campos que se usan en esta consulta Hello son coordenadas GPS de Hola de ubicaciones de recogida y caída, denominados *recogida\_longitud*, *recogida\_latitud*,  *caída\_longitud*, y *caída\_latitud*. las consultas de Hola que calcular Hola distancia directa entre las coordenadas de recogida y caída de hello son:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

ecuaciones matemáticas Hola que calcular la distancia de hello entre dos coordenadas GPS pueden encontrarse en hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">secuencias de comandos de tipo móvil</a> sitio, creado por Peter Lapisu. En su Javascript Hola función `toRad()` es *lat_or_lon*180/pi *, que convierte grados tooradians. En este caso, *lat_or_lon* es Hola latitud o longitud. Puesto que el subárbol no proporciona la función hello `atan2`, pero proporciona la función hello `atan`, hello `atan2` función se implementa mediante `atan` función Hola por encima de la consulta de Hive mediante definición de hello proporcionada en <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Creación del espacio de trabajo](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Una lista completa de Hive UDF incrustadas pueden encontrarse en hello **funciones integradas** sección en hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>Temas avanzados: tooImprove de parámetros de Hive de optimizar la velocidad de consulta
Hola configuración de clúster de Hive podría no ser adecuados para consultas de Hive de Hola y los datos de Hola que se están procesando las consultas de hello un parámetro predeterminado. En esta sección se explican algunos parámetros que los usuarios pueden ajustar que mejoran el rendimiento de Hola de consultas de Hive. Los usuarios necesitan el parámetro de hello tooadd optimizar consultas antes de las consultas de hello del procesamiento de datos.

1. **Espacio de montón de Java**: para las consultas que implican combinar conjuntos de datos grandes o procesar registros largos, **quedando sin espacio en el montón** es uno de los errores comunes de Hola. Esto puede corregirse estableciendo parámetros *mapreduce.map.java.opts* y *mapreduce.task.io.sort.mb* toodesired valores. Aquí tiene un ejemplo:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Este parámetro asigna espacio de montón de tooJava de memoria de 4GB y también realiza la ordenación más eficaz asignando más memoria para él. Es un tooplay buena idea con estas asignaciones si hay un espacio de trabajo error errores tooheap relacionados.

1. **Tamaño de bloque de DFS** : este parámetro establece la unidad más pequeña de Hola de datos que Hola almacenes del sistema de archivos. Por ejemplo, si el tamaño de bloque DFS de hello es 128MB, a continuación, ningún dato de tamaño inferior o superior too128MB se almacena en un único bloque, mientras que los datos que es mayores que 128MB se asigna a bloques adicionales. Elegir un tamaño de bloque muy pequeño hace grandes sobrecargas en Hadoop como nodo de nombre de hello tiene tooprocess muchas más solicitudes toofind Hola relevante bloque pertenecen toohello archivo. Una configuración recomendada al tratar con datos de gigabytes (o mayores) es:
   
        set dfs.block.size=128m;
2. **Optimizar la operación de combinación en el subárbol** : mientras las operaciones de combinación en el marco de trabajo de asignación/reducción de hello normalmente tienen lugar en hello reducir fase, a veces, una enorme puede mejorar mediante la programación de combinaciones en fase de asignación de hello (también denominada "mapjoins"). toodirect subárbol toodo esto siempre que sea posible, podemos establecer:
   
        set hive.auto.convert.join=true;
3. **Especifica el número de Hola de asignadores tooHive** : Hadoop mientras permite Hola usuario tooset Hola número de reductores, el número de Hola de asignadores es normalmente no se establece por usuario de Hola. Un truco que permite cierto grado de control en este número es una variable de Hadoop de hello toochoose, *mapred.min.split.size* y *mapred.max.split.size* como tamaño de Hola de cada asignación de tarea viene determinada por:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Por lo general, Hola valor predeterminado de *mapred.min.split.size* es 0, que de *mapred.max.split.size* es **Long.MAX** y el de *dfs.block.size* es de 64MB. Como podemos ver, tamaño de los datos Hola determinado, estos parámetros "configuración" de ajuste les permite nos tootune Hola número de asignadores usa.
4. A continuación se mencionan algunas otras **opciones avanzadas** más para optimizar el rendimiento de Hive. Estos permiten tooset Hola memoria asignada toomap y reducen las tareas y pueden ser útiles para aumentar el rendimiento. Tenga en cuenta que hello *mapreduce.reduce.memory.mb* no puede ser mayor que el tamaño de memoria física de Hola de cada nodo de trabajo en clúster de Hadoop de Hola.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

