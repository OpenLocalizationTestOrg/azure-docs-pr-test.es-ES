---
title: "Hola proceso de ciencia de datos de equipo en acción: mediante un clúster de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB | Documentos de Microsoft"
description: "Con hello proceso de ciencia de datos de equipo para un escenario de extremo a emplear un Hadoop de HDInsight toobuild de clúster e implementar un modelo con un conjunto de datos disponible públicamente grande de (1 TB)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Hola proceso de ciencia de datos de equipo en acción: mediante un clúster de Hadoop de HDInsight de Azure en un conjunto de datos de 1 TB

En este tutorial, se muestra cómo utilizar Hola proceso de ciencia de datos de equipo en un escenario de extremo a extremo con un [clúster de HDInsight Hadoop de Azure](https://azure.microsoft.com/services/hdinsight/) toostore, explorar, ingeniero de características y el detalle de los datos de ejemplo desde uno de hello públicamente disponible [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjuntos de datos. Aprendizaje automático de Azure toobuild un modelo de clasificación binaria se usa en estos datos. También le mostramos cómo toopublish uno de estos modelos como un servicio Web.

También es posible toouse en este tutorial se presentan una tareas de hello IPython tooaccomplish de Bloc de notas. Los usuarios que serían como tootry debe consultar este enfoque Hola [tutorial Criteo mediante una conexión ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tema.

## <a name="dataset"></a>Descripción del conjunto de datos de Criteo
Hola Criteo datos están un conjunto de datos de predicción de clic es de aproximadamente 370GB de archivos .tsv de gzip comprimido (~1.3TB sin comprimir), que incluye más de 4.3 mil millones de registros. Estos datos proceden de 24 días de datos de clics que ofrece [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Para mayor comodidad de Hola de científicos de datos, se ha descomprimido tooexperiment toous disponibles de datos con.

Cada registro de este conjunto de datos contiene 40 columnas:

* Hola primera columna es una columna de etiqueta que indica si un usuario hace clic en un **agregar** (valor 1) o no haga clic en uno (valor 0)
* Las 13 columnas siguientes son numéricas.
* Las últimas 26 son columnas de categorías.

columnas de Hello son anónimos y utilizar una serie de nombres enumerados: "Col1" (para la columna de etiqueta de hello) demasiado ' Col40 "(para la última columna de categorías hello).            

Este es un extracto de hello primero 20 columnas de dos observaciones (filas) de este conjunto de datos:

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Hay valores que faltan en ambas columnas numéricas y categorías de hello en este conjunto de datos. Se describe un método sencillo para controlar los valores que faltan Hola. Detalles adicionales de los datos de Hola se exploran al almacenarlos en tablas de Hive.

**Definición:** *tasa de Click-through (CTR):* trata Hola porcentaje de clics en los datos de Hola. En este conjunto de datos Criteo, Hola CTR es aproximadamente 3.3% o 0.033.

## <a name="mltasks"></a>Ejemplos de tareas de predicción
En este tutorial, se describen dos problemas de predicción de ejemplo:

1. **Clasificación binaria**: predice si un usuario ha hecho clic o no en un anuncio:
   
   * Clase 0: no hace clic.
   * Clase 1: sí hace clic.
2. **Regresión**: predice la probabilidad de Hola de un clic de ad a partir de funciones de usuario.

## <a name="setup"></a>Configuración de un clúster de Hadoop de HDInsight para la ciencia de los datos
**Nota:** Esta tarea la suelen hacer los **administradores**.

Configure su entorno de ciencia de datos de Azure para crear soluciones de análisis predictivos con los clústeres de HDInsight en tres pasos:

1. [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md): esta cuenta de almacenamiento es toostore usa datos en almacenamiento de blobs de Azure. datos de Hello usados en clústeres de HDInsight se almacenan aquí.
2. [Personalice los clústeres de Hadoop de HDInsight de Azure para la ciencia de los datos](machine-learning-data-science-customize-hadoop-cluster.md): en este paso, se crea un clúster de Hadoop de HDInsight de Azure con Anaconda Python 2.7 de 64 bits instalado en todos los nodos. Al personalizar el clúster de HDInsight de hello, hay toocomplete de dos pasos importantes (descritas en este tema).
   
   * Debe vincular la cuenta de almacenamiento de hello creada en el paso 1 con el clúster de HDInsight cuando se crea. Esta cuenta de almacenamiento se utiliza para tener acceso a datos que pueden ser procesados en el clúster de Hola.
   * Debe habilitar el nodo principal de acceso remoto toohello de clúster de Hola después de crearlo. Recordar las credenciales de acceso remoto de Hola que especifique aquí (que son distintas de las especificadas para el clúster de hello en su creación): vaya necesitando toocomplete Hola procedimientos siguientes.
3. [Crear un área de trabajo de aprendizaje automático de Azure](machine-learning-create-workspace.md): aprendizaje automático de Azure esta área de trabajo se usa para crear modelos de aprendizaje automático después de una exploración de datos iniciales y hacia abajo de muestreo en clúster de HDInsight Hola.

## <a name="getdata"></a>Obtención y consumo de datos desde un origen público
Hola [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjunto de datos puede obtenerse acceso haciendo clic en vínculo hello, acepte las condiciones de uso de Hola y proporcionar un nombre. Aquí se muestra una instantánea de esta pantalla:

![Aceptar los términos de Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Haga clic en **tooDownload continuar** tooread más información sobre el conjunto de datos de Hola y su disponibilidad.

datos de Hello residen en un complemento público [almacenamiento de blobs de Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ubicación: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. Hola "wasb" hace referencia la ubicación de almacenamiento de blobs de tooAzure. 

1. datos de Hello en el almacenamiento de blobs público está formada por tres subcarpetas de datos sin comprimir.
   
   1. Hola subcarpeta *sin formato/count/* contiene Hola primera 21 días de datos, desde el día\_tooday 00\_20
   2. Hola subcarpeta *sin formato/entrenar/* consta de un solo día de datos, día\_21
   3. Hola subcarpeta *sin formato/test/* consta de dos días de datos, día\_22 y día\_23
2. Para aquellos que desean toostart con datos sin formato gzip de hello, también están disponibles en la carpeta principal de hello *sin formato /* como day_NN.gz, donde NN va de too23 00.

Un enfoque alternativo tooaccess, explorar y modele estos datos que no requieren las descargas locales se explica más adelante en este tutorial, cuando se crean tablas de Hive.

## <a name="login"></a>Inicie sesión en el nodo principal del clúster de toohello
toolog en el nodo principal de toohello del clúster de hello, use hello [portal de Azure](https://ms.portal.azure.com) clúster de hello toolocate. Haga clic en icono de hello HDInsight elefante en hello izquierda y, a continuación, haga doble clic en nombre de hello del clúster. Navegue toohello **configuración** ficha, haga doble clic en el icono de conectar hello en parte inferior de Hola de página de Hola y escriba sus credenciales de acceso remoto cuando se le solicite. Esto le llevará el nodo principal de toohello del clúster de Hola.

Este es el aspecto de un primer registro en el nodo principal del clúster de toohello típico:

![Inicie sesión en toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

Hola izquierda, vemos Hola "Hadoop línea de comandos", que es nuestro potente para la exploración de datos de Hola. También vemos dos direcciones URL útiles: "Hadoop Yarn Status" (Estado de Hadoop Yarn) y "Hadoop Name Node" (Nombre del nodo de Hadoop). dirección URL de Hello yarn estado muestra el progreso del trabajo y URL del nodo de nombre de hello proporciona detalles sobre la configuración de clúster de Hola.

Ahora se configura y está listo toobegin primera parte del tutorial de Hola: exploración de datos con Hive y preparar datos para aprendizaje automático de Azure.

## <a name="hive-db-tables"></a> Creación de tablas y base de datos de Hive
toocreate Hive tablas para el conjunto de datos Criteo, abra hello ***línea de comandos de Hadoop*** en Hola escritorio del nodo principal de Hola y escriba el directorio del subárbol de hello escribiendo el comando de Hola

    cd %hive_home%\bin

> [!NOTE]
> Ejecutar todos los comandos de Hive en este tutorial de Papelera de Hive Hola / símbolo del sistema de directorio. De esta manera, cualquier problema con la ruta de acceso se soluciona automáticamente. Usamos Hola términos "Prompt de directorio de Hive", "Hive bin / símbolo del sistema de directorio" y "línea de comandos de Hadoop" indistintamente.
> 
> [!NOTE]
> tooexecute cualquier consulta de Hive, siempre se pueden usar Hola siguientes comandos:
> 
> 

        cd %hive_home%\bin
        hive

Después de hello Hive REPL aparece con un "hive >" iniciar sesión, corte y pegue Hola consulta tooexecute lo.

Hello código siguiente crea una base de datos "criteo" y, a continuación, genera 4 tablas:

* un *tabla para generar recuentos* creado en el día de días\_tooday 00\_20,
* un *tabla para su uso como conjunto de datos de entrenamiento de Hola* basado en día\_21, y
* dos *conjuntos de datos de prueba de tablas para su uso como hello* basado en día\_22 y día\_23 respectivamente.

El conjunto de datos de prueba se divide en dos tablas diferentes porque uno de los días de hello es un día festivo, y queremos toodetermine si el modelo de Hola puede detectar las diferencias entre un día festivo y no de vacaciones de velocidad de Click-through de Hola.

Hola script [ejemplo &#95; hive &#95; crear &#95; criteo &#95; base de datos &#95; y &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) se muestra aquí por comodidad:

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

Se tenga en cuenta que todas estas tablas son externas como podemos simplemente punto tooAzure ubicaciones de almacenamiento de blobs (wasb).

**Hay dos maneras tooexecute Hive cualquier consulta que mencionamos ahora.**

1. **Usar Hola Hive REPL de línea de comandos**: hello en primer lugar es tooissue un comando "hive" y copie y pegue una consulta al Hola Hive REPL de línea de comandos. toodo este, no:
   
        cd %hive_home%\bin
        hive
   
     Consulta de hello ejecuta ahora en hello REPL de línea de comandos, cortar y pegar.
2. **Guardar consultas tooa archivo y ejecutar el comando de hello**: hello en segundo lugar está el archivo .hql tooa de toosave hello las consultas ([ejemplo &#95; hive &#95; crear &#95; criteo &#95; base de datos &#95; y &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) y, a continuación, siguiente de Hola de problema comando consulta de Hola tooexecute:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Confirmación de la creación de la tabla y la base de datos
A continuación, se confirme la creación de hello de base de datos de hello con hello siguiente comando desde la Papelera de Hive Hola / símbolo del sistema de directorio:

        hive -e "show databases;"

Este es el resultado:

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Esto confirma la creación de hello de base de datos nueva hello, "criteo".

toosee qué tablas que hemos creado, se emite simplemente Hola comando aquí desde la Papelera de Hive Hola / símbolo del sistema de directorio:

        hive -e "show tables in criteo;"

A continuación, vemos Hola después de salida:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> Exploración de datos en Hive
Ahora estamos listos toodo una exploración de datos básicos en el subárbol. Se empezar contando Hola número de ejemplos de entrenamiento de Hola y tablas de datos de prueba.

### <a name="number-of-train-examples"></a>Número de ejemplos de "train"
Hola contenido de [ejemplo &#95; hive &#95; recuento &#95; entrenar &#95; tabla &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) se muestran a continuación:

        SELECT COUNT(*) FROM criteo.criteo_train;

El resultado es:

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

O bien, uno puede emitir también Hola siguiente comando desde la Papelera de Hive Hola / símbolo del sistema de directorio:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Número de ejemplos de prueba de hello dos conjuntos de datos de prueba
Ahora contamos con número Hola de ejemplos de conjuntos de datos de dos pruebas Hola. Hola contenido de [ejemplo &#95; hive &#95; recuento &#95; criteo &#95; prueba &#95; día &#95; 22 &#95; tabla &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) aquí:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

El resultado es:

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

Como es habitual, también podemos llamarlo script de Hola de Papelera de Hive Hola / directory símbolo del sistema mediante la emisión de comandos de hello:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Por último, examinamos número Hola de ejemplos de prueba de conjunto de datos de prueba de hello en función de día\_23.

Hello toodo de comando es similar toohello una muestra (consulte demasiado[ejemplo &#95; hive &#95; recuento &#95; criteo &#95; prueba &#95; día &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Este es el resultado:

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Distribución de etiqueta en el conjunto de datos de entrenamiento de Hola
distribución de la etiqueta de Hello en el conjunto de datos de entrenamiento de hello es de interés. toosee esto, se muestra el contenido de [ejemplo &#95; hive &#95; criteo &#95; etiqueta &#95; distribución &#95; entrenar &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Esto da como resultado la distribución de la etiqueta de hello:

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Tenga en cuenta que Hola porcentaje de las etiquetas positivas es 3.3% (coherente con el conjunto de datos original de hello).

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Distribuciones de histograma de algunas variables numéricas en hello entrenar el conjunto de datos
Podemos usar nativo del subárbol "histograma\_numérico" función toofind out qué distribución Hola de variables numéricas hello es similar. Estos son contenido Hola de [ejemplo &#95; hive &#95; criteo &#95; histograma &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

Esto da como resultado siguiente hello:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

Hola LATERAL vista - seccionar combinación en Hive actúa tooproduce una salida similar a SQL en lugar de lista de saludo habitual. Tenga en cuenta que en Hola esta tabla, la primera columna de hello corresponde toohello bin hello y center segundo toohello bin frecuencia.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Percentiles aproximados de algunas variables numéricas en hello entrenar el conjunto de datos
Además de interés con variables numéricas es cálculo Hola de percentiles aproximados. La función nativa de Hive "percentile\_approx" permite realizar esta acción. Hola contenido de [ejemplo &#95; hive &#95; criteo &#95; aproximado &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) son:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

El resultado es:

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

Se Comente que distribución Hola de percentiles suele toohello estrechamente relacionadas con el histograma distribución de cualquier variable numérica.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Buscar el número de valores únicos para algunas columnas de categorías en el conjunto de datos de entrenamiento de Hola
Continuar con la exploración de datos de hello, encontramos ahora, para algunas columnas de categorías, número de Hola de valores únicos que se necesitan. toodo esto, se muestra el contenido de [ejemplo &#95; hive &#95; criteo &#95; único &#95; valores &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

El resultado es:

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Tenga en cuenta que Col15 tiene 19 millones de valores únicos. Usar técnicas de naïve como "estrechamente con una codificación" tooencode dichas variables de categorías muy dimensionales es factible. En particular, vamos a explicar y mostrar una técnica eficaz y contundente llamada [Aprendizaje con recuentos](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) para hacer frente a este problema de forma eficaz.

Esta subsección se finalizar examinando Hola número de valores únicos para algunas otras columnas de categorías también. Hola contenido de [ejemplo &#95; hive &#95; criteo &#95; único &#95; valores &#95; varios &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) son:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

El resultado es:

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Nuevo vemos que excepto Col20, todos Hola otras columnas tienen muchos valores únicos.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Recuentos de repetición coadministradores de pares de variables de categorías en el conjunto de datos de entrenamiento de Hola

Hola coadministradores repeticiones de pares de variables de categorías también es de interés. Esto se puede determinar mediante código de hello en [ejemplo &#95; hive &#95; criteo &#95; emparejada &#95; categorías &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

Se invertir orden Hola recuentos por su aparición y busque en la parte superior de hello 15 en este caso. El resultado obtenido es el siguiente:

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Hacia abajo de conjuntos de datos de ejemplo hello para el aprendizaje automático de Azure
Tener Hola explorar conjuntos de datos y muestra cómo podemos hacer este tipo de exploración de las variables (incluidas combinaciones), que ahora hacia abajo de conjuntos de datos de ejemplo Hola por lo que podemos crear modelos de aprendizaje automático de Azure. Recuerde error Hola nos centramos en es: dado un conjunto de atributos de ejemplo (valores de las características de Col2 - Col40), se predecir si Col1 es un 0 (no haga clic en) o 1 (hacer clic).

toodown ejemplo nuestro entrenar y probar los conjuntos de datos too1% del tamaño original de hello, usamos una función RAND() nativa del subárbol. Hola la siguiente secuencia de comandos, [ejemplo &#95; hive &#95; criteo &#95; disminuir la resolución &#95; entrenar &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) hace conjunto de datos de entrenamiento de hello:

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

El resultado es:

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Hola script [ejemplo &#95; hive &#95; criteo &#95; disminuir la resolución &#95; prueba &#95; día &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) lo hace para los datos de prueba, día\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

El resultado es:

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Por último, Hola script [ejemplo &#95; hive &#95; criteo &#95; disminuir la resolución &#95; prueba &#95; día &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) lo hace para los datos de prueba, día\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

El resultado es:

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

Con esto, se está listo toouse nuestro abajo muestrea entrenar y probar los conjuntos de datos para generar modelos de aprendizaje automático de Azure.

Hay un componente importante final antes de seguir adelante tooAzure aprendizaje automático, que es la tabla de recuento de hello preocupaciones. En hello siguiente subsección, se explican con más detalle.

## <a name="count"></a>Obtener una breve descripción en la tabla de recuento de Hola
Como hemos visto, algunas variables de categorías tienen una dimensionalidad muy alta. En nuestro tutorial, le presentaremos una técnica eficaz denominada [aprendizaje con recuentos](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode estas variables de una manera eficaz y sólida. Para obtener más información sobre esta técnica está en vínculo Hola proporcionado.

[!NOTE]
>En este tutorial, se centran en el uso de recuento tablas tooproduce compact representaciones de las características de categorías muy dimensionales. Esto no es Hola única manera tooencode las características de categorías; Para obtener más información sobre otras técnicas, los usuarios interesados pueden extraer del repositorio [uno-activos-encoding](http://en.wikipedia.org/wiki/One-hot) y [hash de características](http://en.wikipedia.org/wiki/Feature_hashing).
>

tablas de recuento de toobuild en datos de la cuenta de hello, utilizamos datos de Hola Hola/sin formato de carpeta de recuento. Hola modelado sección, se muestran a los usuarios cómo toobuild estas funciones cuentan las tablas para las características de categorías desde cero o, alternativamente, toouse una tabla de recuento pregenerado para sus exploraciones. En lo que se indica a continuación, cuando se hace referencia demasiado "previamente generado tablas de recuento", nos referimos usando tablas de recuento de Hola que ofrecemos. Instrucciones detalladas sobre cómo tooaccess estas tablas se proporcionan en la sección siguiente Hola.

## <a name="aml"></a> Creación de modelos con el Aprendizaje automático de Azure
Nuestro proceso de creación de modelos con Azure Machine Learning consta de estos pasos:

1. [Obtener datos de Hola de las tablas de Hive en aprendizaje automático de Azure](#step1)
2. [Crear experimento de hello: limpiar datos de Hola y caracterizar con tablas de recuento](#step2)
3. [Compilación, entrenar y modelo de puntuación Hola](#step3)
4. [Evaluar el modelo de Hola](#step4)
5. [Publicar el modelo de Hola como un servicio web](#step5)

Ahora estamos listos toobuild modelos en estudio de aprendizaje automático de Azure. Los datos muestreados abajo se guardan como tablas de Hive en clúster de Hola. Usamos Hola aprendizaje automático de Azure **importar datos** tooread módulo estos datos. cuenta de almacenamiento de Hello credenciales tooaccess Hola de este clúster se muestran en qué se indica a continuación.

### <a name="step1"></a>Paso 1: Obtener datos de las tablas de Hive en aprendizaje mediante el módulo de importación de datos de Hola y selecciónelo para un experimento de aprendizaje automático
Para empezar, seleccione **+NUEVO** -> **EXPERIMENTO** -> **Experimento en blanco**. A continuación, en hello **búsqueda** cuadro en hello esquina superior izquierda, busque "Importar datos". Hola de arrastrar y colocar **importar datos** módulo en módulo toohello experimento lienzo (parte media de Hola de pantalla de bienvenida) toouse hello para el acceso a datos.

Esto es qué hello **importar datos** aspecto al obtener datos de tabla de Hive hello:

![Importar datos obtiene los datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Para hello **importar datos** módulo, valores de hello de parámetros de Hola que se proporcionan en hello gráfico son sólo algunos ejemplos de hello, tipo de valores necesita tooprovide. Aquí tiene algunas instrucciones generales acerca toofill parámetro hello de salida de hello **importar datos** módulo.

1. Elija "Consulta de Hive" como **Origen de datos**
2. Hola **consulta de base de datos de Hive** cuadro, una instrucción SELECT simple * FROM < su\_base de datos\_name.your\_tabla\_name >-es suficiente.
3. **URI del servidor de Hcatalog**: si el clúster es "abc", este valor simplemente será: https://abc.azurehdinsight.net
4. **Nombre de cuenta de usuario de Hadoop**: nombre de usuario de hello seleccionado en el momento de Hola de puesta en servicio de Cluster Server de Hola. (No Hola acceso remoto nombre de usuario!)
5. **Contraseña de cuenta de usuario de Hadoop**: Hola contraseña Hola nombre de usuario seleccionado en el momento de Hola de puesta en servicio de Cluster Server de Hola. (No Hola contraseña de acceso remoto!)
6. **Ubicación de los datos de salida**: elija "Azure".
7. **Nombre de la cuenta de almacenamiento de Azure**: Hola cuenta de almacenamiento asociada con el clúster de Hola
8. **Clave de cuenta de almacenamiento de Azure**: clave Hola de hello cuenta de almacenamiento asociada con el clúster de Hola.
9. **Nombre de contenedor de Azure**: si el nombre del clúster de hello es "abc", esto suele ser simplemente "abc",.

Una vez Hola **importar datos** termina de obtención de datos (ver graduación Hola verde en hello módulo), guardar estos datos como un conjunto de datos (con un nombre de su elección). Este es el aspecto:

![Importar datos guarda los datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Puerto de hello de salida de hello contextual **importar datos** módulo. Se muestran las opciones **Guardar como conjunto de datos** y **Visualizar**. Hola **visualizar** opción, si hace clic en, muestra 100 filas de datos de hello, junto con un panel derecho que es útil para algunas estadísticas de resumen. datos de toosave, simplemente seleccione **Guardar como conjunto de datos** y siga las instrucciones.

tooselect Hola guardan conjunto de datos para su uso en un experimento de aprendizaje de máquina, buscar conjuntos de datos de hello mediante hello **búsqueda** cuadro se muestra en la figura siguiente de Hola. A continuación, sólo tiene que escribir el nombre de Hola se le asignó hello conjunto de datos parcialmente tooaccess y arrastre Hola conjunto de datos a Hola panel principal. Colocar en el panel principal de hello, selecciona para su uso en el modelado de aprendizaje de máquina.

![Conjunto de datos de arrastre en el panel principal Hola](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Hágalo para entrenar hello y conjuntos de datos de prueba de Hola. También, recuerde el nombre de base de datos de toouse hello y nombres de tabla que ha asignado para este propósito. valores de Hello utilizados en la figura Hola son únicamente para ilustración purposes.* *
> 
> 

### <a name="step2"></a>Paso 2: Crear un experimento sencillo en aprendizaje automático de Azure toopredict clics / no hace clic en
Nuestro experimento de Azure Machine Learning tiene el siguiente aspecto:

![Experimento de Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

Ahora se examinan los componentes clave de Hola de este experimento. Como recordatorio, necesitamos toodrag nuestro guardado entrenar y probar los conjuntos de datos en el lienzo del experimento de tooour primero.

#### <a name="clean-missing-data"></a>Limpiar datos que faltan
Hola **limpiar datos que faltan** módulo lo que sugiere su nombre: limpia los datos que faltan de manera que puede ser especificado por el usuario. En este módulo, veremos estos datos:

![Limpiar datos que faltan](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

En este caso, elegimos tooreplace todos los valores que faltan con un 0. Hay otras opciones, que pueden ser vistos examinando las listas desplegables de hello en el módulo de Hola.

#### <a name="feature-engineering-on-hello-data"></a>Característica de ingeniería en datos de Hola
Puede haber millones de valores únicos para algunas características de categoría de grandes conjuntos de datos. El uso de métodos simples como la codificación "one-hot" para representar estas características de categorías no es viable. En este tutorial, se muestra cómo las características de recuento de toouse con toogenerate de módulos de aprendizaje automático de Azure integrada compact representaciones de estas variables de categorías muy dimensionales. Hello resultado final es un tamaño más pequeño de modelo, velocidad de entrenamiento y las métricas de rendimiento que son bastante comparable toousing otras técnicas.

##### <a name="building-counting-transforms"></a>Creación de transformaciones de recuento
funciones de recuento de toobuild, se usa los hello **compilar contando transformar** módulo que está disponible en aprendizaje automático de Azure. módulo de Hello tiene el siguiente aspecto:

![Módulo Crear transformación de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Módulo Crear transformación de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> Hola **el número de columna** cuadro, escribimos las columnas que se desea tooperform cuenta. Normalmente, son columnas de categorías con una alta dimensionalidad (tal y como se mencionó). En el inicio de hello, mencionamos ese conjunto de datos de Criteo hello tiene 26 columnas de categorías: de Col15 tooCol40. En este caso, se cuentan en todos ellos y proporcionar a sus índices (de 15 too40 separados por comas, como se muestra).
> 

módulo de hello toouse en Hola MapReduce modo (adecuado para grandes conjuntos de datos), necesitamos accedemos clúster de Hadoop de HDInsight tooan (Hola uno utilizado para la exploración de la característica se puede reutilizar para este propósito así) y sus credenciales. figuras anterior de Hello muestran qué valores rellena Hola apariencia (reemplazar valores de hello dan a modo ilustrativo con los que son relevantes para su propio caso de uso).

![Parámetros del módulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

En la ilustración de hello anterior, mostramos cómo tooenter Hola entrada blob ubicación. Esta ubicación tiene datos Hola reservados para la creación de tablas de recuento.

Una vez finaliza la ejecución de este módulo, podemos guardar transformación Hola para más tarde haciendo clic en el módulo de Hola y seleccionar hello **Guardar como transformación** opción:

![Opción "Guardar como transformación"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

En nuestra arquitectura de experimento mostrado anteriormente, Hola dataset "ytransform2" corresponde exactamente tooa guarda la transformación de recuento. Para el resto de Hola de este experimento, suponemos que ese lector hello usa un **compilar contando transformar** módulo en algunos datos toogenerate recuentos y, a continuación, puede usar las características de recuento de recuentos toogenerate en tren de Hola y conjuntos de datos de prueba.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>Elegir qué cuenta tooinclude características como parte del entrenamiento de Hola y conjuntos de datos de prueba
Una vez que tenemos un recuento transformar listo, usuario Hola puede elegir qué tooinclude características en su entrenar y probar los conjuntos de datos mediante hello **modificar parámetros de tabla de recuento** módulo. Mostramos este módulo a continuación solo para ofrecer una visión completa, pero para simplificar no lo usamos en nuestro experimento.

![Parámetros de la tabla de modificación de recuentos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

En este caso, tal y como se puede ver, que hemos elegido toouse probabilidades de registro solo Hola y Hola tooignore retroceder de columna. También podemos establecer parámetros como Hola umbral de Papelera, cuántos tooadd ejemplos pseudo anterior para suavizar, y si toouse cualquier Laplaciana ruido o no. Todos estos son características avanzados y es toobe en cuenta que los valores predeterminados de hello son un buen punto de partida para los usuarios que son el nuevo tipo de toothis de generación de la característica.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Transformación de datos antes de generar características de recuento de Hola
Ahora se centrarse en un punto importante acerca de la transformación nuestro entrenar y probar datos tooactually anterior generar características de recuento. Tenga en cuenta que hay dos **ejecutar Script de R** módulos usados para aplicar la transformación tooour datos de recuento de Hola.

![Ejecución de módulos de script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Este es el primer script de R hello:

![Primer script de R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

En este script de R, cambiamos el nombre de nuestro toonames columnas "Col1" demasiado "Col40". Esto es porque la transformación recuento de hello espera que los nombres de este formato.

El segundo script de R hello, se un equilibrio entre la distribución de Hola entre clases positivas y negativas (clases 1 y 0, respectivamente) por clase de disminución de resolución Hola negativo. Hola R este script muestra cómo toodo esto:

![Segundo script de R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

En esta secuencia de comandos de R simple, se utiliza "pos\_neg\_proporción" cantidad de hello tooset de equilibrio entre las clases negativo de Hola y Hola positivo. Esto es importante toodo ya que suele mejorar el desequilibrio de la clase tiene ventajas de rendimiento para problemas de clasificación donde la distribución de la clase de hello es sesgado (Recuerde que en nuestro caso, tenemos 3.3% positivo clase y clase negativo 96,7%).

##### <a name="applying-hello-count-transformation-on-our-data"></a>Aplicar transformación de recuento de hello en nuestros datos
Por último, podemos usar hello **aplicar transformación** tooapply módulo Hola transformaciones de recuento en nuestro entrenar y probar los conjuntos de datos. Este módulo toma la transformación recuento de hello guardado como una entrada y Hola entrenar o probar los conjuntos de datos como Hola otra entrada y devuelve los datos con características de recuento. Se muestra aquí:

![Módulo Aplicar transformación](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Un extracto del aspecto de características de recuento de Hola
Es instructivo toosee qué características de recuento de hello aspecto en nuestro caso. Aquí se muestra un extracto de esto:

![Características de recuento](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

En este extracto, se mostrará que para las columnas de Hola que se enumeran en, se obtener recuentos de Hola y probabilidades de registro en suma tooany relevante backoffs.

Ahora estamos listo toobuild un modelo de aprendizaje automático de Azure con estos conjuntos de datos transformados. En la siguiente sección hello, mostramos cómo puede hacerlo.

### <a name="step3"></a>Paso 3: Crear, entrenar y puntuar modelo Hola

#### <a name="choice-of-learner"></a>Elección del aprendiz
En primer lugar, necesitamos toochoose un aprendiz. Estamos continuo toouse un árbol de decisión impulsado de dos clases como nuestro aprendiz. Estas son opciones predeterminadas de Hola para este aprendiz:

![Parámetros de árbol de decisiones incrementados de dos clases](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

Para nuestro experimento, estamos valores predeterminados de curso toochoose Hola. Se tenga en cuenta que hello tiene como valor predeterminado son normalmente significativa y una buena manera tooget rápido las líneas de base en el rendimiento. Puede mejorar en el rendimiento mediante el barrido de parámetros si elige tooonce que tiene una línea base.

#### <a name="train-hello-model"></a>Entrenar el modelo de Hola
Para el entrenamiento, simplemente invocamos un módulo **Entrenar modelo** . Hola dos entradas tooit son aprendiz de árbol de decisión impulsado de dos clases de Hola y el conjunto de datos de entrenamiento. Esto se muestra a continuación:

![Módulo Entrenar modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Modelo de Hola de puntuación
Una vez que tenemos un modelo entrenado, estamos preparados tooscore en hello probar el conjunto de datos y tooevaluate su rendimiento. Esto se realiza mediante hello **puntuar modelo** módulo se muestra en hello siguiente figura, junto con un **evaluar modelo** módulo:

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>Paso 4: Evaluar el modelo de Hola
Por último, nos gustaría tooanalyze rendimiento del modelo. Por lo general, para los dos problemas de clasificación (binaria) de clase, una buena medida es hello AUC. toovisualize esto, se enlazó hello **puntuar modelo** módulo tooan **evaluar modelo** módulo para esto. Haga clic en **visualizar** en hello **evaluar modelo** módulo da como resultado un gráfico como Hola sigue uno:

![Módulo Evaluación del modelo de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

En binario (o clase dos) problemas de clasificación, una buena medida de precisión de la predicción se Hola área en curva (AUC). A continuación, mostramos nuestros resultados al usar este modelo en nuestro conjunto de datos "test". tooget, puerto de salida de hello contextual de hello **evaluar modelo** módulo y, a continuación, **visualizar**.

![Visualización del módulo Evaluar modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>Paso 5: Publicar modelo Hola como un servicio Web
Hola capacidad toopublish un modelo de aprendizaje automático de Azure como servicios web con un mínimo de molestias es una característica útil para realizar ampliamente disponibles. Una vez hecho esto, cualquier usuario puede crear el servicio web de llamadas a toohello con datos de entrada que necesiten predicciones para y servicio web de hello usa Hola modelo tooreturn estas predicciones.

toodo, guardamos primero nuestro modelo de aprendizaje como un objeto de modelo entrenado. Esto se hace con el botón secundario hello **entrenar modelo** módulo y usar hello **Guardar como modelo entrenado** opción.

A continuación, necesitamos toocreate entrada y salida de puertos para el servicio web:

* un puerto de entrada toma los datos en hello mismo formulario como datos de Hola que necesitamos predicciones para
* un puerto de salida devuelve Hola puntuación de etiquetas y las probabilidades de hello asociado.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Seleccione algunas filas de datos para el puerto de entrada de Hola
Es conveniente toouse una **aplicar transformación de SQL** módulo tooselect simplemente 10 filas tooserve como Hola los datos de puerto de entrada. Seleccione solo estas filas de datos para nuestro puerto de entrada mediante consultas SQL Hola que se muestra a continuación:

![Datos del puerto de entrada](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Servicio web
Ahora estamos listos toorun un experimento pequeño que puede ser utilizado toopublish nuestro servicio web.

#### <a name="generate-input-data-for-webservice"></a>Generación de datos de entrada para el servicio web
Como paso cero, puesto que es grande, la tabla de recuento de Hola se tardar unas pocas líneas de datos de prueba y generan datos de salida a partir de él con características de recuento. Esto puede servir como formato de datos de entrada de Hola de nuestro servicio Web. Esto se muestra a continuación:

![Creación de datos de entrada de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Para el formato de datos de entrada de hello, usamos ahora Hola salida de hello **Count Featurizer** módulo. Una vez que esto experimentar termine la ejecución, guardar la salida de hello de hello **Count Featurizer** módulo como un conjunto de datos. Este conjunto de datos se utiliza para los datos de entrada de hello en hello webservice.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Puntuación del experimento para la publicación del servicio web
En primer lugar, veamos el aspecto que tiene. Hola esencial estructura es una **puntuar modelo** módulo que acepta el objeto de modelo entrenado y unas pocas líneas de datos de entrada que se generan en pasos anteriores de hello con hello **Count Featurizer** módulo. Se utiliza "Seleccionar columnas de conjunto de datos" tooproject Hola puntuado etiquetas y las probabilidades de puntuación de Hola.

![Seleccionar columnas de conjunto de datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Tenga en cuenta cómo Hola **seleccionar columnas de conjunto de datos** módulo puede utilizarse para 'filtrando' datos de un conjunto de datos. Se muestra contenido de hello aquí:

![Filtrar con hello seleccionar columnas en el módulo de conjunto de datos](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

puertos de hello azul de entrada y salida tooget, simplemente haga clic en **preparar webservice** final Hola derecho. Ejecuta este experimento también permite que nos toopublish Hola servicio web: haga clic en hello **publicar servicio WEB** situado en aquí de derecho, como se muestra de la parte inferior de hello:

![Publicar servicio web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Una vez publicado el servicio Web de hello, obtenemos tooa redirigida página que busca por lo tanto:

![Panel del servicio web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

Dos vínculos de servicios Web se muestra en el lado izquierdo de hello:

* Hola **solicitud/respuesta** servicio (o RR) está destinados solo predicciones y es lo que se usan en el taller.
* Hola **ejecución por lotes** servicio (BES) se utiliza para las predicciones por lotes y requiere que las predicciones de toomake de datos de entrada utilizados Hola residan en almacenamiento de blobs de Azure.

Al hacer clic en el vínculo de hello **solicitud/respuesta** nos lleva tooa página que nos da predefinidos previamente el código en C#, python y R. Este código se puede usar de forma cómoda para realizar llamadas toohello webservice. Tenga en cuenta que Hola clave de API en esta página debe toobe utilizado para la autenticación.

Es conveniente toocopy este python código sobre tooa nueva celda en el Bloc de notas de IPython Hola.

Aquí mostramos un segmento de código python con clave de API de hello correcta.

![Código de Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Tenga en cuenta que reemplazamos clave de API de hello predeterminada con la clave de API de nuestros servicios Web. Haga clic en **ejecutar** en esta celda en una IPython Bloc de notas, da como resultado Hola después de respuesta:

![Respuesta de IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Se puede ver que para hello dos pruebas ejemplos que pedimos sobre (en el marco de trabajo JSON de hello del script de python Hola), obtenemos respuestas en forma de Hola "Puntuado etiquetas, las probabilidades de puntuado". Tenga en cuenta que en este caso, elegimos valores predeterminados de hello ese código predefinida Hola proporciona (0 para todas las columnas numéricas y cadena Hola "value" para todas las columnas de categorías).

Con esto concluye nuestra tutorial to-end que se muestra cómo toohandle dataset a gran escala mediante el aprendizaje automático de Azure. Trabajar con un terabyte de datos, crea un modelo de predicción y había implementado como un servicio web en la nube de Hola.

