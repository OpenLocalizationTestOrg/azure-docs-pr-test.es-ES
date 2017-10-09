---
title: aaaCreate tablas de Hive y cargar datos desde almacenamiento de blobs de Azure | Documentos de Microsoft
description: Crear tablas de Hive y cargar datos en tablas de toohive de blob
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Creación de tablas de Hive y carga de datos desde Azure Blob Storage
En este tema se presentan consultas genéricas de Hive que crean tablas de Hive y cargan datos desde Azure Blob Storage. También se proporciona alguna orientación acerca de las particiones de tablas de Hive y sobre cómo utilizar Hola optimizado fila columnas (ORC) formato tooimprove rendimiento de las consultas.

Esto **menú** vincula tootopics que describen cómo tooingest datos en entornos de destino donde se pueden almacenar y procesar durante datos Hola Hola proceso de ciencia de datos de equipo (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que ha:

* Creado una cuenta de almacenamiento de Azure. Para obtener instrucciones, vea [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).
* Aprovisionar un clúster de Hadoop personalizado con hello servicio HDInsight.  Si necesita instrucciones, consulte [Personalización de clústeres de Hadoop de HDInsight de Azure para análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).
* Clúster de toohello de acceso remoto habilitado, se registran en y abre la consola de línea de comandos de Hadoop de Hola. Si necesita instrucciones, consulte [Hola de acceso principal del nodo de clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Cargar el almacenamiento de blobs de datos tooAzure
Si ha creado una máquina virtual de Azure siguiendo las instrucciones de hello proporcionadas en [configurar una máquina virtual de Azure para análisis avanzado](machine-learning-data-science-setup-virtual-machine.md), el archivo de script debería haber sido descargado toohello *C:\\ Los usuarios\\\<nombre de usuario\>\\documentos\\secuencias de comandos de ciencia de datos* directorio en la máquina virtual de Hola. Estas consultas de Hive solo requieren que conecte en su propio esquema de datos y la configuración de almacenamiento de blobs de Azure en hello campos correspondientes toobe listo para el envío.

Se supone que los datos de Hola para las tablas de subárbol están en un **sin comprimir** formato tabular, y que los datos de hello ha sido cargado predeterminado de toohello (o tooan adicional) contenedor de hello cuenta de almacenamiento utilizado por el clúster de Hadoop de Hola.

Si desea que toopractice en hello **NYC Taxi recorridos datos**, necesita:

* **descargar** Hola 24 [NYC Taxi recorridos datos](http://www.andresmh.com/nyctaxitrips) archivos (12 archivos de ida y vuelta y 12 archivos tarifa),
* **Descomprima** todos los archivos en archivos .csv.
* **cargar** ellos predeterminado toohello (o contenedor adecuado) de Hola cuenta de almacenamiento de Azure que se creó mediante el procedimiento de hello descrito en hello [para el proceso de análisis avanzado y la tecnología de clústeres de Hadoop de HDInsight de Azure de personalizar ](machine-learning-data-science-customize-hadoop-cluster.md) tema. Hola proceso tooupload Hola .csv archivos toohello contenedor predeterminado en la cuenta de almacenamiento de hello puede encontrarse en el objeto [página](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>¿Cómo toosubmit consultas de Hive
Las consultas de subárbol se pueden enviar mediante:

1. [Enviar consultas de Hive a través de línea de comandos de Hadoop en el nodo principal del clúster de Hadoop](#headnode)
2. [Enviar consultas de Hive con hello Editor de Hive](#hive-editor)
3. [Enviar consultas de Hive con los comandos de Azure PowerShell](#ps)

Las consultas de Hive son similares a SQL. Si está familiarizado con SQL, es posible hello [Hive para hoja de referencia rápida de los usuarios de SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) útil.

Al enviar una consulta de Hive, también puede controlar el destino de Hola de salida de hello de las consultas de Hive, ya sea en la pantalla o tooa archivo local de hello en el nodo principal de Hola o tooan blobs de Azure.

### <a name="headnode"></a> 1. Enviar consultas de Hive a través de línea de comandos de Hadoop en el nodo principal del clúster de Hadoop
Si Hola Hive consulta es compleja, enviar que directamente en el nodo principal de Hola de clúster de Hadoop de hello conduce normalmente a su vez toofaster alrededor de envío con un Editor de Hive o secuencias de comandos de PowerShell de Azure.

Inicie sesión en toohello nodo principal del clúster de Hadoop de hello, abra Hola línea de comandos de Hadoop en el escritorio de hello del nodo principal de Hola y escriba el comando `cd %hive_home%\bin`.

Tiene consultas de Hive de tres maneras toosubmit Hola línea de comandos de Hadoop:

* Directamente
* usando archivos .hql
* con hello Hive consola de comandos

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Envíe consultas de subárbol directamente en la línea de comandos de Hadoop.
Puede ejecutar el comando como `hive -e "<your hive query>;` toosubmit consultas sencillas de Hive directamente en Hadoop línea de comandos. Este es un ejemplo, donde hello rojo un contorno alrededor Hola comando que envía la consulta de Hive de Hola y Hola recuadro verde contornos Hola resultados de consulta de Hive Hola.

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Enviar consultas de subárbol en archivos .hql
Cuando la consulta de Hive hello es más complicado y tiene varias líneas, la modificación de consultas en la línea de comandos o la consola de comandos de Hive no resulta práctico. Una alternativa es toouse un editor de texto en el nodo principal de Hola de consultas de Hive de hello toosave clúster de Hadoop hello en un archivo .hql en un directorio local del nodo principal de Hola. A continuación, la consulta de Hive hello en el archivo de hello .hql puede enviarse mediante hello `-f` argumento tal como sigue:

    hive -f "<path toohello .hql file>"

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Suprimir la impresión de pantalla del estado de progreso de las consultas de subárbol**

De forma predeterminada, una vez enviada en línea de comandos de Hadoop, en la consulta de Hive progreso de Hola de trabajo de asignación y reducción de Hola se imprime en pantalla. toosuppress Hola imprimir pantalla de progreso del trabajo de asignación y reducción de hello, puede usar un argumento `-S` ("S" en mayúsculas) en hello línea de comandos como se indica a continuación:

    hive -S -f "<path toohello .hql file>"
.    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Envíe consultas de subárbol en la consola de comandos de subárbol.
En primer lugar también puede escribir consola de comandos del subárbol de hello mediante la ejecución de comando `hive` en línea de comandos de Hadoop y, a continuación, enviar consultas de Hive en la consola de comandos de Hive. Aquí tiene un ejemplo. En este ejemplo, hello dos cuadros rojos resaltado Hola comandos usados tooenter Hola consola de comandos de Hive y Hola consulta de Hive enviada en la consola de comandos de Hive, respectivamente. cuadro de Hello verde resalta la salida de hello de consulta de Hive Hola.

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

en los ejemplos anteriores Hola directamente resultados Hola Hive consulta en pantalla. También puede escribir tooa de archivo local en el nodo principal de Hola o tooan blobs de Azure para la salida Hola. A continuación, puede usar otras herramientas toofurther analizar la salida de hello de consultas de Hive.

**Salida de archivo local de tooa de resultados de consulta de Hive.**
toooutput Hive consultar resultados tooa local en el directorio en el nodo principal de hello, tiene consulta de Hive toosubmit Hola Hola línea de comandos de Hadoop como se indica a continuación:

    hive -e "<hive query>" > <local path in hello head node>

En el siguiente ejemplo de Hola, se escribe la salida de hello de consulta de Hive en un archivo `hivequeryoutput.txt` en el directorio `C:\apps\temp`.

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Salida tooan de resultados de consulta de Hive blobs de Azure**

También puede generar Hola Hive consulta resultados tooan blob de Azure, dentro de contenedor de hello predeterminado del clúster de Hadoop de Hola. consulta de Hive de Hola para esto es el siguiente:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

En el siguiente ejemplo de Hola, salida de hello de consulta de Hive se escribe el directorio de blob tooa `queryoutputdir` dentro de contenedor de hello predeterminado del clúster de Hadoop de Hola. En este caso, solo necesita tooprovide nombre del directorio hello, sin nombre de blob de Hola. Se produce un error si proporciona los nombres de directorio y de blob, como `wasb:///queryoutputdir/queryoutput.txt`.

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Si abre el contenedor predeterminado de Hola de clúster de Hadoop de hello mediante el Explorador de almacenamiento de Azure, puede ver la salida de hello de consulta de Hive Hola tal y como se muestra en la figura siguiente de Hola. Puede aplicar Hola filtro (resaltado mediante cuadro rojo) tooonly recuperar Hola blob con letras especificadas en los nombres.

![Creación del espacio de trabajo](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Enviar consultas de Hive con hello Editor de Hive
También puede utilizar Hola consola de consultas (Editor de Hive) mediante la especificación de una dirección URL de formulario de hello *https://&#60; Nombre del clúster de Hadoop >.azurehdinsight.net/Home/HiveEditor* en un explorador web. Debe ser iniciado en hello, vea esta consola y por lo que necesita las credenciales de clúster de Hadoop.

### <a name="ps"></a> 3. Enviar consultas de Hive con los comandos de Azure PowerShell
También puede utilizar consultas de Hive toosubmit de PowerShell. Para obtener instrucciones, consulte [Envío de trabajos de Hive mediante PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Creación de tablas y base de datos de Hive
Hello consultas de Hive compartidas hello [repositorio de GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) y puede descargarse desde allí.

Aquí es la consulta de Hive de Hola que crea una tabla de Hive.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Estas son las descripciones de Hola de campos de Hola que necesite tooplug en y otras configuraciones:

* **&#60; nombre de base de datos >**: nombre de Hola de base de datos de Hola que desea toocreate. Si su intención es base de datos predeterminada de toouse hello, Hola consulta *crear base de datos...*  puede omitirse.
* **&#60; nombre de tabla >**: nombre de Hola de tabla de Hola que desea toocreate dentro de la base de datos especificada de Hola. Si desea que la base de datos predeterminada de toouse hello, tabla de hello puede hacer referencia directamente mediante *&#60; nombre de tabla >* sin &#60; nombre de base de datos >.
* **&#60; separador de campos >**: separador de Hola que delimita los campos de toobe de archivo de datos de hello cargado toohello tabla de Hive.
* **&#60; separador de línea >**: separador de Hola que delimita las líneas en el archivo de datos de hello.
* **&#60; ubicación de almacenamiento >**: Hola datos de almacenamiento de Azure ubicación toosave Hola de tablas de Hive. Si no se especifica *ubicación &#60; ubicación de almacenamiento >*, Hola base de datos y tablas hello se almacenan una en *hive/almacenamiento/* directorio en el contenedor de hello predeterminado del clúster de Hive Hola de forma predeterminada. Si desea que la ubicación de almacenamiento de toospecify hello, ubicación de almacenamiento de hello tiene toobe dentro de contenedor de hello predeterminado para la base de datos de Hola y tablas. Esta ubicación tiene toobe hace referencia como contenedor de ubicación relativa toohello predeterminado del clúster de hello en formato de Hola de *' wasb: / / / &#60; directorio 1 > /'* o *' wasb: / / / &#60; directorio 1 > / &#60; directorio 2 > /'*, etcetera. Cuando se ejecuta la consulta de hello, directorios relativa Hola se crean dentro del contenedor predeterminado de Hola.
* **TBLPROPERTIES("Skip.Header.Line.Count"="1")**: si el archivo de datos de hello tiene una línea de encabezado, tienen tooadd esta propiedad **final hello** de hello *crear tabla* consulta. En caso contrario, se carga la línea de encabezado de hello como una tabla de registro toohello. Si el archivo de datos de hello no tiene una línea de encabezado, se puede omitir esta configuración en la consulta de Hola.

## <a name="load-data"></a>Cargar datos tooHive tablas
Aquí es la consulta de Hive de Hola que carga datos en una tabla de Hive.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; datos de ruta de acceso tooblob >**: Hola si Hola blob archivo toobe cargado toohello Hive tabla está en el contenedor de predeterminado de Hola de hello clúster de Hadoop de HDInsight, *&#60; datos de ruta de acceso tooblob >* debe estar en formato de Hola *' wasb: / / / &#60; directorio de este contenedor > / &#60; nombre de archivo de blob >'*. archivo de blob de Hello también puede estar en un contenedor adicional de hello clúster de Hadoop de HDInsight. En este caso, *&#60; datos de ruta de acceso tooblob >* debe estar en formato de hello *' wasb: / / &#60; nombre de contenedor > @&#60; nombre de la cuenta de almacenamiento >.blob.core.windows.net/ &#60; nombre de archivo de blob >'*.

  > [!NOTE]
  > Hello toobe cargado tooHive tabla de datos de blob tiene toobe en predeterminado de Hola o contenedor adicional de la cuenta de almacenamiento de hello para el clúster de Hadoop de Hola. En caso contrario, Hola *carga datos* consulta produce un error que indica que el que no se puede tener acceso a datos de Hola.
  >
  >

## <a name="partition-orc"></a>Temas avanzados: tabla con particiones y datos de Hive de almacén en formato ORC
Si hello es grande, creación de particiones de tabla de hello es beneficioso para las consultas que solo necesitan tooscan algunas particiones de tabla de Hola. Por ejemplo, son datos de registro de hello toopartition razonable de un sitio web por fechas.

En suma toopartitioning Hive tablas, así como datos de Hive de hello toostore beneficioso en formato de optimizado fila columnas (ORC) de Hola. Para obtener más información acerca de la aplicación de formato ORC, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">El uso de archivos ORC mejora el rendimiento cuando Hive está leyendo, escribiendo y procesando datos</a>.

### <a name="partitioned-table"></a>Tabla con particiones
Aquí es la consulta de Hive de Hola que crea una tabla con particiones y carga datos en él.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Al consultar tablas con particiones, se recomienda tooadd condición de partición Hola Hola **principio** de hello `where` cláusula que esta mejora la eficacia de Hola de búsqueda de forma significativa.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Almacenamiento de datos de Hive en formato ORC
No se puede cargar directamente datos desde almacenamiento de blobs en tablas de subárbol que se almacena en formato de hello ORC. Estos son los pasos de hello tablas tooHive almacenadas en formato ORC los blobs en ese Hola necesita tootake tooload datos de Azure.

Cree una tabla externa **almacenados archivo de texto de AS** y cargar datos de tabla de toohello de almacenamiento de blobs.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Crear una tabla interna con hello mismo esquema que la tabla externa de hello en el paso 1, con hello mismo el delimitador de campo y almacenar Hola datos de Hive en formato de hello ORC.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Seleccionar datos de la tabla externa de hello en el paso 1 e insertar en la tabla de hello ORC

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Si tabla del archivo de texto hello *&#60; nombre de base de datos >. &#60; nombre de la tabla de archivo de texto externo >* tiene particiones, en el paso 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando selecciona Hola variable de partición como un campo de hello devuelve el conjunto de datos. Insertándolo en hello *&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >* se produce un error desde *&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >* no tiene la variable de la partición de Hola como un campo de esquema de la tabla de Hola. En este caso, deberá toospecifically Hola seleccione campos toobe insertar demasiado*&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >* como se indica a continuación:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

Es seguro toodrop hello *&#60; nombre de la tabla de archivo de texto externo >* cuando Hola después de consulta después de todos los datos de uso se ha insertado en *&#60; nombre de base de datos >. &#60; nombre de la tabla ORC >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Después de seguir este procedimiento, debe tener una tabla con datos en hello ORC formato listo toouse.  
