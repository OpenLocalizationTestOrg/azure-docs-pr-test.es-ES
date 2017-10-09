---
title: aaaOverview de ciencia de datos con Spark en HDInsight de Azure | Documentos de Microsoft
description: "Kit de herramientas de Hello Spark MLlib pone aprendizaje automático considerable de capacidades toohello distribuida HDInsight entorno de modelado."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Información general sobre la ciencia de los datos con Spark en HDInsight de Azure
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Este conjunto de temas muestra cómo toouse ciencia de datos común de HDInsight Spark toocomplete tareas como la recopilación de datos, la ingeniería de característica, modelado y evaluación de modelos. datos de Hello usa están un ejemplo de Hola 2013 NYC taxi tarifas y recorridos conjunto de datos. modelos de Hello integrados incluyen regresión logística y lineal, los bosques aleatorios y los árboles impulsados degradados. Hello temas también muestra cómo toostore estos modelos en Azure blob storage (WASB) y cómo tooscore y evaluar su rendimiento predictivo. En los temas más avanzados se describe cómo se pueden entrenar los modelos mediante validación cruzada y barrido de hiperparámetros. Este tema de Introducción también hace referencia a temas de Hola que describen cómo tooset seguridad Hola clúster Spark que necesitan pasos de hello toocomplete en los tutoriales de hello proporcionado. 

## <a name="spark-and-mllib"></a>Spark y MLlib
[Spark](http://spark.apache.org/) es un marco de trabajo de procesamiento paralelo de código abierto que admite en memoria tooboost Hola rendimiento de aplicaciones analíticas de grandes cantidades de datos del procesamiento. motor de procesamiento de Hello Spark se compila para acelerar el proceso, facilidad de uso y análisis sofisticados. Capacidades de cálculo distribuido en memoria de Spark representan una buena elección para los algoritmos iterativo hello usa en los cálculos de aprendizaje y de máquina. [MLlib](http://spark.apache.org/mllib/) es entorno distribuido de toothis capacidades de modelado de biblioteca de aprendizaje de máquina escalable de Spark que aporta Hola algorítmica. 

## <a name="hdinsight-spark"></a>HDInsight Spark
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) es hello hospedado de Azure de la oferta de Spark de código abierto. También incluye compatibilidad para **Jupyter PySpark blocs de notas** en clúster de Spark Hola que se puede ejecutar las consultas interactivas de Spark SQL para transformar, filtrar y visualizar los datos almacenados en Blobs de Azure (WASB). PySpark es hello API de Python para Spark. fragmentos de código de Hello que ofrecen soluciones de Hola y muestran Hola relevante traza toovisualize Hola datos aquí se ejecute en blocs de notas de Jupyter instalados en los clústeres de Spark Hola. pasos de modelado de Hello en los temas siguientes contienen código que muestra cómo tootrain, evaluar, guardar y consumir cada tipo de modelo. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Programa de instalación: clústeres de Spark e instancias de Jupyter Notebooks
Los pasos de instalación y el código proporcionado en este tutorial son para HDInsight Spark 1.6. Sin embargo, Jupyter Notebooks se proporciona para clústeres de HDInsight Spark 1.6 y Spark 2.0. Se proporciona una descripción de hello blocs de notas y vínculos toothem Hola [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para el repositorio de GitHub de Hola que los contienen. Además, código de hello aquí y en blocs de notas de hello vinculada genérica y debe funcionar en cualquier clúster de Spark. Si no utilizas HDInsight Spark, pasos de configuración y administración de clúster de hello pueden ser ligeramente diferentes de lo que se muestra aquí. Para mayor comodidad, estos son Hola vínculos toohello Jupyter portátiles con Spark 1.6 (toobe ejecutar en el núcleo de pySpark Hola de hello servidor de Jupyter Notebook) y Spark 2.0 (se ejecuta en el núcleo de pySpark3 Hola de servidor de Jupyter Notebook hello toobe):

### <a name="spark-16-notebooks"></a>Cuadernos de Spark 1.6
Estos equipos portátiles son toobe ejecutar en el núcleo de pySpark Hola de servidor de Jupyter notebook.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): proporciona información acerca de cómo tooperform la exploración de datos, modelado y puntuación con varios algoritmos.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): incluye temas sobre el cuaderno 1 y sobre el desarrollo de modelos mediante el ajuste de hiperparámetros y la validación cruzada.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): muestra cómo toooperationalize un modelo guardado con Python en HDInsight de clústeres.

### <a name="spark-20-notebooks"></a>Cuadernos de Spark 2.0
Estos equipos portátiles son toobe ejecutar en el núcleo de pySpark3 Hola de servidor de Jupyter notebook.

- [Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este archivo proporciona información sobre cómo tooperform la exploración de datos, modelado y puntuación en Spark 2.0 clústeres utilizando Hola recorridos Taxi de Nueva York y se describe de conjunto de datos tarifa [aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Este bloc de notas puede ser un buen punto de partida para analizar rápidamente el código de hello que se proporcionan para Spark 2.0. Para un bloc de notas más detallada analiza Hola datos Taxi de Nueva York, consulte Bloc de notas siguiente hello en esta lista. Vea las notas de hello después de la lista que comparan estos blocs de notas. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): este archivo muestra cómo tooperform datos problemas con (Spark SQL y trama de datos de operaciones), la exploración, modelado y puntuación mediante Hola tarifas conjunto de datos se describe y recorridos de Nueva York Taxi [ aquí](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): este archivo muestra cómo tooperform datos problemas con (Spark SQL y trama de datos de operaciones), la exploración, modelado y puntuación mediante Hola conocido salida en el momento de Airline conjunto de datos de 2011 y 2012. El conjunto de datos de hello airline se habían integrado con hello aeropuerto tiempo datos (por ejemplo, velocidad del viento, temperatura, altitud, etc.) anteriores toomodeling para que estas características de tiempo pueden incluirse en el modelo de Hola.

<!-- -->

> [!NOTE]
> el conjunto de datos de Hello airline agregó blocs de notas toohello Spark 2.0 toobetter ilustran el uso de Hola de algoritmos de clasificación. Vea Hola siguientes vínculos para obtener información sobre el conjunto de datos de salida en el momento de airline y conjunto de datos de tiempo:

>- Datos de salida puntuales de líneas aéreas: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Datos climatológicos del aeropuerto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
blocs de notas de Hello Spark 2.0 en hello taxi de Nueva York y airline vuelo retraso conjuntos de datos pueden tardar 10 minutos o más toorun (según el tamaño de Hola de su clúster HDI). Hello primer portátil Hola por encima de la lista muestra muchos aspectos Hola de exploración de datos, visualización y aprendizaje automático del modelo de entrenamiento en un portátil que toma menos toorun de tiempo con muestrear abajo NYC conjunto de datos, en qué Hola taxi y tarifa que se hayan archivos previamente combinados: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) este bloc de notas toma una cantidad menor tiempo toofinish (2-3 minutos) y puede ser un buen punto de partida para analizar rápidamente el código de hello tenemos se proporcionan para Spark 2.0. 

<!-- -->

Para obtener instrucciones sobre la puesta en marcha de un modelo de Spark 2.0 y el consumo de modelo para puntuar hello, vea hello [documento Spark 1.6 consumo de](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) para obtener un ejemplo de esquematización pasos Hola necesarios. toouse esto en Spark 2.0, reemplace el archivo de código Python de hello con [este archivo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Requisitos previos
Hola siguiendo los procedimientos es tooSpark relacionado 1.6. Para la versión de Hola Spark 2.0, use blocs de notas de Hola se describían y vinculado toopreviously. 

1. Debe tener una suscripción de Azure. Si aún no tiene una, consulte [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)(Obtener una evaluación gratuita de Azure).

2. se necesita un toocomplete de clúster de Spark 1.6 en este tutorial. toocreate uno, consulte las instrucciones de hello proporcionadas en [Introducción: crear Apache Spark en HDInsight de Azure](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). tipo de clúster de Hola y la versión se especifica en hello **Seleccionar tipo de clúster** menú. 

![Configuración del inicio de sesión del clúster](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Para un tema que muestra cómo toouse Scala en lugar de Python toocomplete las tareas de un proceso de ciencia de datos to-end, vea hello [ciencia de datos con Scala Spark en Azure](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Hola datos NYC 2013 Taxi
Hola datos NYC Taxi recorridos es de aproximadamente 20 GB comprimido valores separados por comas (CSV) de archivos de (~ 48 GB sin comprimir), que incluye más de 173 millones hello y viajes individuales puntuación de pago para cada recorrido. Cada registro de ida y vuelta incluye Hola recogerá y ubicación de entrega y hora, hack anonimizado (controlador) el número de licencia y medallion (identificador único del taxi) número. datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:

1. archivos CSV de Hello 'trip_data' contienen detalles de ida y vuelta, como el número de los pasajeros, recoger y caída apunta, viaje duración y la duración del viaje. Estos son algunos registros de ejemplo:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. archivos CSV de Hello 'trip_fare' contienen detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago. Estos son algunos registros de ejemplo:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Le hemos llevado un ejemplo de 0,1% de estos archivos y recorridos de hello combinadas\_datos y recorridos\_resultados son archivos CVS en un único conjunto de datos toouse como conjunto de datos de entrada de Hola para este tutorial. recorridos de toojoin de clave única de Hello\_datos y recorridos\_tarifa se compone de campos de hello: medallion, prueba\_licencia y recogida\_fecha y hora. Cada registro del conjunto de datos de hello contiene Hola siguientes atributos que representa un viaje de Nueva York Taxi:

| Campo | Breve descripción |
| --- | --- |
| medallion |Licencias de taxi anónimas (identificador único del taxi) |
| hack_license |Número de licencia anónima de taxi londinense |
| vendor_id |Identificador del proveedor del taxi |
| rate_code |Categoría de tarifa de taxi de Nueva York |
| store_and_fwd_flag |Indicador de “guardar y reenviar” |
| pickup_datetime |Fecha y hora de subida |
| dropoff_datetime |Fecha y hora de bajada |
| pickup_hour |Hora de recogida |
| pickup_week |Recoger la semana del año de Hola |
| weekday |Día de la semana (intervalo de 1 a 7) |
| passenger_count |Número de pasajeros en una carrera de taxi |
| trip_time_in_secs |Tiempo de la carrera, en segundos |
| trip_distance |Distancia recorrida en la carrera, en millas |
| pickup_longitude |Longitud del punto de subida |
| pickup_latitude |Latitud del punto de subida |
| dropoff_longitude |Longitud del punto de bajada |
| dropoff_latitude |Latitud del punto de bajada |
| direct_distance |Distancia directa entre las ubicaciones de subida y bajada |
| payment_type |Tipo de pago (efectivo, tarjeta de crédito, etc.) |
| fare_amount |Importe de la tarifa en |
| surcharge |Suplemento |
| mta_tax |Impuestos de MTA |
| tip_amount |Importe de la propina |
| tolls_amount |Importe de los peajes |
| total_amount |Importe total |
| tipped |Con propina (0 o 1 para No o Sí) |
| tip_class |Clase de propina (0: 0 $, 1: 0-5 $, 2: 6-10 $, 3: 11-20 $, 4: > 20 $) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Ejecutar el código desde Jupyter notebook en clúster de Spark Hola
Puede iniciar hello Jupyter Notebook de hello portal de Azure. Busque su clúster Spark en el panel y haga clic en página de administración de tooenter para el clúster. Haga clic en Bloc de notas de tooopen Hola asociado con el clúster de Spark hello, **paneles de clúster** -> **Jupyter Notebook** .

![Paneles de clúster](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

También puede examinar demasiado***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess Hola Jupyter blocs de notas. Reemplace la parte del nombre del clúster de Hola de esta dirección URL por nombre de Hola de su propio clúster. Es necesaria la contraseña de Hola para los administradores cuenta tooaccess Hola blocs de notas.

![Examinar cuadernos de Jupyter Notebook](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

Seleccione PySpark toosee un directorio que contiene algunos ejemplos de los blocs de notas preconfiguradas que usar hello PySpark API.hello blocs de notas que contienen ejemplos de código de hello para este conjunto de tema de Spark están disponibles en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

Puede cargar directamente desde blocs de notas de hello [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) toohello de servidor de Jupyter notebook en su clúster Spark. En página de inicio de Hola de su Jupyter, haga clic en hello **cargar** botón en hello parte derecha de la pantalla de bienvenida. Se abre un explorador de archivos. Aquí puede pegar la dirección URL de GitHub (contenido sin formato) de Hola de hello Bloc de notas y haga clic en **abiertos**. 

Vea el nombre de archivo de hello en la lista de archivos de Jupyter con un **cargar** nuevamente en el botón. Haga clic en este botón **Cargar** . Ahora ha importado el Bloc de notas de Hola. Repita estos Hola de tooupload pasos otros blocs de notas de este tutorial.

> [!TIP]
> Puede hacer clic vínculos hello en el explorador y seleccione **Copiar vínculo** tooget Hola dirección URL de contenido sin procesar de github. Puede pegar esta dirección URL en el cuadro de diálogo de explorador de archivos de Jupyter cargar de Hola.
> 
> 

Ahora puede:

* Ver código de hello haciendo clic en el Bloc de notas de Hola.
* Ejecutar cada celda presionando **MAYÚS+ENTRAR**.
* Ejecutar el Bloc de notas completo Hola haciendo clic en **celda** -> **ejecutar**.
* Usar Hola visualización automática de las consultas.

> [!TIP]
> núcleo de Hello PySpark automáticamente visualiza la salida de hello de consultas SQL (HiveQL). Se proporcionan Hola opción tooselect entre distintos tipos de visualizaciones (tabla, circular, línea, el área o barra) mediante el uso de hello **tipo** botones de menú en el Bloc de notas de hello:
> 
> 

![Curva ROC de regresión logística para el enfoque genérico](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>Pasos siguientes
Ahora que se han configurado con un clúster de HDInsight Spark y han cargado los blocs de notas de Jupyter hello, está listo toowork a través de temas de Hola que corresponden toohello tres PySpark portátiles. Muestran cómo tooexplore los datos y, a continuación, cómo toocreate y consumir los modelos. Hola avanzada de exploración de datos y modelado Bloc de notas muestra cómo tooinclude validación cruzada, un parámetro de hyper barrido y evaluación de modelos. 

**Exploración de datos y el modelado con Spark:** explorar el conjunto de datos de Hola y crear, puntuación y evaluar modelos de aprendizaje automático de Hola por trabajar a través de hello [crear modelos de clasificación y regresión binarios para datos con hello Spark Kit de herramientas de MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) tema.

**Consumo de modelo:** toolearn cómo crean modelos de clasificación y regresión de hello tooscore en este tema, consulte [puntuación y evaluar modelos de aprendizaje automático integrado Spark](machine-learning-data-science-spark-model-consumption.md).

**Validación cruzada y barrido de hiperparámetros**: consulte [Exploración y modelado avanzados de datos con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) sobre cómo pueden prepararse los modelos con el barrido de hiperparámetros y la validación cruzada.

