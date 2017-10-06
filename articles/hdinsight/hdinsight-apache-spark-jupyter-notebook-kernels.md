---
title: "clústeres de aaaKernels para Jupyter notebook en Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información sobre los kernels de hello PySpark, PySpark3 y Spark para Jupyter notebook disponible con clústeres de Spark en HDInsight de Azure."
keywords: Jupyter Notebook en Spark, Spark en Jupyter
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Kernels para Jupyter Notebook en clústeres Spark en Azure HDInsight 

Los clústeres de HDInsight Spark proporcionan kernels que puede usar con el Bloc de notas de hello Jupyter en Spark para probar las aplicaciones. Un kernel es un programa que ejecuta e interpreta el código. los kernels de tres Hola son:

- **PySpark** (para aplicaciones escritas en Python2)
- **PySpark3** (para aplicaciones escritas en Python3)
- **Spark** (para aplicaciones escritas en Scala)

En este artículo, aprenderá cómo toouse estos kernels y las ventajas de Hola de su uso.

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Creación de un cuaderno de Jupyter Notebook en clústeres Spark de HDInsight

1. De hello [portal de Azure](https://portal.azure.com/), abra el clúster.  Vea [lista y mostrar los clústeres de](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) para obtener instrucciones de Hola. clúster de Hola se abre en una nueva hoja de portal.

2. De hello **vínculos rápidos** sección, haga clic en **paneles de clúster** tooopen hello **paneles de clúster** hoja.  Si no ve **vínculos rápidos**, haga clic en **Introducción** desde el menú de la izquierda hello en la hoja de Hola.

    ![Jupyter Notebook en Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Jupyter Notebook en Spark") 

3. Haga clic en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.
   
   > [!NOTE]
   > También puede tener acceso a Jupyter notebook de hello en clúster de Spark por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Haga clic en **New**y, a continuación, haga clic en **Pyspark**, **PySpark3**, o **Spark** toocreate un bloc de notas. Usar el kernel de Spark Hola para aplicaciones Scala, kernel PySpark para aplicaciones de Python2 y PySpark3 kernel para aplicaciones de Python3.
   
    ![Kernels de Jupyter Notebook en Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Kernels de Jupyter Notebook en Spark") 

4. Se abre un bloc de notas con kernel Hola que seleccionó.

## <a name="benefits-of-using-hello-kernels"></a>Ventajas de utilizar los kernels de Hola

Estas son algunas ventajas de usar kernels nuevos Hola con Jupyter notebook en clústeres de HDInsight Spark.

- **Contextos preestablecidos**. Con **PySpark**, **PySpark3**, o hello **Spark** kernels, no es necesario tooset Hola Spark o subárbol contextos explícitamente antes de empezar a trabajar con las aplicaciones. ya que están disponibles de forma predeterminada. Estos contextos son:
   
   * **sc** : para el contexto Spark
   * **sqlContext** : para el contexto Hive

    Por lo tanto, no tiene instrucciones de toorun como Hola siguientes contextos de Hola tooset:

        sc = SparkContext('yarn-client')  sqlContext = HiveContext(sc)

    En su lugar, puede usar directamente Hola preestablecido contextos de la aplicación.

- **Instrucciones mágicas de celda**. Hello PySpark kernel proporciona algunos predefinidas "magics", que son comandos especiales que se pueden llamar con `%%` (por ejemplo, `%%MAGIC` <args>). comando mágica Hola debe ser Hola primera palabra en una celda de código y permitir varias líneas de contenido. word mágica Hola debe ser primera palabra en la celda de Hola de Hola. Agregar cualquier cosa antes de magia hello, incluso de los comentarios, producirá un error.     Para obtener más información sobre instrucciones mágicas, vaya [aquí](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Hello tabla siguiente enumeran magics diferentes de hello disponibles a través de los kernels de Hola.

   | Instrucción mágica | Ejemplo | Description |
   | --- | --- | --- |
   | help |`%%help` |Genera una tabla de todos los magics disponibles Hola con ejemplo y la descripción |
   | info |`%%info` |Genera información de sesión para el punto de conexión de hello actual Livio |
   | CONFIGURAR |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Configura los parámetros de Hola para crear una sesión. Hola marca force (-f) es obligatorio si ya se ha creado una sesión, lo que garantiza que esa sesión Hola se quita y vuelve a crear. Consulte [Livy's POST /sessions Request Body (Cuerpo de la solicitud de sesiones o POST de Livy)](https://github.com/cloudera/livy#request-body) para obtener una lista de parámetros válidos. Parámetros deben pasarse con como una cadena JSON y deben estar en línea siguiente de hello después magia hello, como se muestra en la columna de ejemplo de Hola. |
   | sql |`%%sql -o <variable name>`<br> `SHOW TABLES` |Ejecuta una consulta de Hive en hello sqlContext. Si hello `-o` se pasa el parámetro, resultado de hello de consulta de Hola se conserva en hello %% contexto Python local como un [Pandas](http://pandas.pydata.org/) trama de datos. |
   | local |`%%local`<br>`a=1` |Todo el código de hello en las líneas siguientes se ejecuta localmente. Código debe ser válido código Python2 incluso independientemente del kernel de Hola que usa. Así, incluso si ha seleccionado **PySpark3** o **Spark** kernels al crear el Bloc de notas de hello, si usas hello `%%local` mágico en una celda, esa celda solo debe tener código Python2 válido... |
   | logs |`%%logs` |Salidas Hola registros de sesión de Livio actual Hola. |
   | delete |`%%delete -f -s <session number>` |Elimina una sesión específica del punto de conexión de hello actual Livio. Tenga en cuenta que no se puede eliminar la sesión para el propio núcleo Hola Hola que se inicia. |
   | cleanup |`%%cleanup -f` |Elimina todas las sesiones del Hola Hola Livio punto de conexión actual, incluida la sesión de este bloc de notas. Hola force marca -f es obligatorio. |

   > [!NOTE]
   > Además toohello magics agregado kernel PySpark de hello, también puede usar hello [integrados magics IPython](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), incluido `%%sh`. Puede usar hello `%%sh` mágico toorun scripts y bloques de código en el nodo principal del clúster de Hola.
   >
   >
2. **Visualización automática**. Hola **Pyspark** kernel automáticamente visualiza la salida de hello de consultas de Hive y SQL. Puede elegir entre diferentes tipos de visualizaciones, como tabla, circular, línea, área o barra.

## <a name="parameters-supported-with-hello-sql-magic"></a>Parámetros compatibles con hello %% mágico de sql
Hola `%%sql` mágico es compatible con parámetros diferentes que puede usar el tipo de hello toocontrol de salida que recibe cuando se ejecutan consultas. Hello en la tabla siguiente muestra la salida de hello.

| Parámetro | Ejemplo | Description |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Utilice este resultado de hello toopersist de parámetro de consulta de hello, Hola %% contexto local de Python, como un [Pandas](http://pandas.pydata.org/) trama de datos. Hola de variable de la trama de datos de Hola se denomina nombre de variable de Hola que especifique. |
| -q |`-q` |Utilice este tooturn desactivar visualizaciones de celda Hola. Si no desea tooauto-visualizar contenido Hola de una celda y sólo desea toocapture como una trama de datos, a continuación, utilice `-q -o <VARIABLE>`. Si desea tooturn desactivar visualizaciones sin capturar resultados hello (por ejemplo, para ejecutar una consulta SQL, como un `CREATE TABLE` instrucción), utilice `-q` sin especificar un `-o` argumento. |
| -m |`-m <METHOD>` |Donde **METHOD** puede ser **take** o **sample** (el valor predeterminado es **take**). Si es el método hello **tomar**, kernel Hola toma los elementos de la parte superior de Hola Hola datos de conjunto de resultados especificado por MAXROWS (descrita más adelante en esta tabla). Si es el método hello **ejemplo**, kernel Hola muestrea de forma aleatoria los elementos del conjunto de datos de hello según demasiado`-r` parámetro, se describe a continuación en esta tabla. |
| -r |`-r <FRACTION>` |Aquí **FRACTION** es un número de punto flotante entre 0,0 y 1,0. Si es el método de ejemplo de Hola para consultas SQL de hello `sample`, a continuación, kernel Hola muestrea fracción especificada de Hola de elementos de Hola de resultado de hello establecen automáticamente de forma aleatoria. Por ejemplo, si ejecuta una consulta SQL con argumentos de hello `-m sample -r 0.01`, muestreo al azar de los 1% Hola de filas de resultados. |
| -n |`-n <MAXROWS>` |**MAXROWS** es un valor entero. núcleo de Hello limita el número de Hola de filas de salida de demasiado**MAXROWS**. Si **MAXROWS** es un número negativo como **-1**, a continuación, Hola número de filas en el conjunto de resultados de hello no está limitado. |

**Ejemplo:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

instrucción de Hello anterior Hola siguientes:

* Selecciona todos los registros de **hivesampletable**.
* Dado que se usa -q, desactiva la visualización automática.
* Dado que usamos `-m sample -r 0.1 -n 500` aleatoriamente muestrea el 10% de filas de hello en hello hivesampletable y límites de tamaño de filas de too500 de conjuntos de resultados de Hola de Hola.
* Por último, dado que hemos usado `-o query2` también guarda la salida de hello en una trama de datos denominado **consulta2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Consideraciones al usar Hola kernels nuevos

El kernel usa, dejando portátiles que Hola ejecutan consume recursos de clúster de Hola.  Con estos núcleos, porque están predefinidos contextos de hello, simplemente salir blocs de notas de hello no kill contexto hello y, por tanto, los recursos de clúster de hello continuar toobe en uso. Una buena práctica es hello de toouse **cerrar y detener la** opción de Bloc de notas hello **archivo** menú cuando haya terminado de usar el Bloc de notas de hello, que elimina el contexto de hello y, a continuación, cierra Hola Bloc de notas.     

## <a name="show-me-some-examples"></a>Estos son algunos ejemplos:

Cuando se abre Jupyter notebook, verá dos carpetas disponibles en el nivel de raíz de Hola.

* Hola **PySpark** carpeta tiene blocs de notas de ejemplo que use Hola nueva **Python** kernel.
* Hola **Scala** carpeta tiene blocs de notas de ejemplo que use Hola nueva **Spark** kernel.

Puede abrir hello **00 - [leer Léame primero] Spark magia Kernel características** Bloc de notas de hello **PySpark** o **Spark** carpeta toolearn sobre magics diferentes de hello disponibles. También puede usar Hola otros blocs de notas de ejemplo disponibles en hello dos carpetas toolearn cómo tooachieve distintos escenarios utilizando blocs de notas de Jupyter con clústeres de HDInsight Spark.

## <a name="where-are-hello-notebooks-stored"></a>¿Dónde se almacenan los blocs de notas de hello?

Jupyter blocs de notas se guardan toohello cuenta de almacenamiento asociada a clúster de hello en hello **/HdiNotebooks** carpeta.  Blocs de notas, archivos de texto y las carpetas que se crean desde dentro de Jupyter son accesibles desde la cuenta de almacenamiento de Hola.  Por ejemplo, si usa una carpeta del Jupyter toocreate **MiCarpeta** y un bloc de notas **myfolder/mynotebook.ipynb**, puede tener acceso a ese portátil a `/HdiNotebooks/myfolder/mynotebook.ipynb` dentro de la cuenta de almacenamiento de Hola.  Hola inversa también es true, es decir, si carga un bloc de notas directamente la cuenta de almacenamiento de tooyour `/HdiNotebooks/mynotebook1.ipynb`, también es visible desde Jupyter notebook Hola.  Blocs de notas permanecen en la cuenta de almacenamiento de hello incluso después de que se elimina el clúster de Hola.

forma de Hello blocs de notas se guardan toohello cuenta de almacenamiento es compatible con HDFS. Por lo tanto, si se SSH en clúster de hello que puede usar comandos de administración del archivo tal y como se muestra en el siguiente fragmento de código de hello:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


En caso de que hay problemas de acceso a la cuenta de almacenamiento de hello para el clúster de hello, blocs de notas de hello también se guardan en el nodo principal de hello `/var/lib/jupyter`.

## <a name="supported-browser"></a>Explorador compatible

Los cuadernos de Jupyter Notebook que se ejecutan en clústeres Spark de HDInsight solo son compatibles con Google Chrome.

## <a name="feedback"></a>Comentarios
Hola y kernels nuevos están en constante evolución fase se maduran con el tiempo. También podría significar que las API podrían cambiar a medida que estos kernels maduran. Agradecemos cualquier comentario que tenga al utilizar estos nuevos kernels. Esto es útil para dar forma al lanzamiento final de Hola de estos núcleos. Puede dejar los comentarios en hello **comentarios** sección Hola final de este artículo.

## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar solicitudes de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)
