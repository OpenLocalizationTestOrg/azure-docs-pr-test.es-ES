---
title: aaaUse Ambari vistas toowork con Hive en HDInsight (Hadoop) - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola Hive vista de las consultas de Hive de toosubmit de explorador web. Hola Hive vista forma parte de hello que ambari Web UI proporcionado con el clúster de HDInsight basados en Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Usar hello vista Hive con Hadoop en HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Obtenga información acerca de cómo las consultas que utilizan la vista del subárbol Ambari toorun Hive. Ambari es una utilidad de administración y supervisión proporcionada con los clústeres de HDInsight basados en Linux. Una de las características de hello proporcionados a través de Ambari es una interfaz de usuario Web que pueden ser consultas de Hive toorun usado.

> [!NOTE]
> Ambari cuenta con muchas funcionalidades que no se tratan en este documento. Para obtener más información, consulte [HDInsight administrar clústeres mediante el uso de hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de HDInsight basado en Linux Para información sobre la creación de un clúster, consulte [Introducción a HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="open-hello-hive-view"></a>Abrir la vista del subárbol de Hola

También puede Ambari vistas de hello portal de Azure; Seleccione el clúster de HDInsight y, a continuación, seleccione **Ambari vistas** de hello **vínculos rápidos** sección.

![sección de vínculos rápidos de portal de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

En lista de Hola de vistas, seleccione hello __Hive vista__.

![Hola vista Hive seleccionada](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Cuando se obtiene acceso a Ambari, son tooauthenticate solicitadas toohello sitio. Escriba Hola, administrador (valor predeterminado `admin`) cuenta de nombre y la contraseña que utilizó al crear Hola clúster.

Debería ver un toohello similar de página después de la imagen:

![Imagen de hoja de cálculo de consulta de hello para la vista del subárbol de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Ejecución de una consulta

toorun una consulta de hive, utilice Hola siguiendo los pasos de la vista del subárbol de Hola.

1. De hello __consulta__ ficha, pegue Hola siguiendo las instrucciones de HiveQL en la hoja de cálculo de hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Estas instrucciones realizan Hola siguientes acciones:

   * `DROP TABLE`-Elimina tabla hello y archivo de datos de hello, en caso de hello tabla ya existe.

   * `CREATE EXTERNAL TABLE`: crea una nueva tabla "externa" en Hive.
   Tablas externas almacenan solo la definición de tabla hello en el subárbol. Hola datos permanecen en la ubicación original de Hola.

   * `ROW FORMAT`-Cómo se da formato a los datos de Hola. En este caso, los campos de hello en cada registro están separados por un espacio.

   * `STORED AS TEXTFILE LOCATION`-Donde se almacenan los datos de Hola y que se almacena como texto.

   * `SELECT`-Selecciona un recuento de todas las filas donde t4 columna contiene el valor de hello [ERROR].

     > [!NOTE]
     > Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo. Por ejemplo, un proceso de carga de datos automatizado u otra operación de MapReduce. Quitar una tabla externa *no* eliminar datos de hello, solo la definición de tabla Hola.

    > [!IMPORTANT]
    > Deje hello __base de datos__ selección __predeterminado__. ejemplos de Hola en este documento utiliza base de datos de hello predeterminada incluida con HDInsight.

2. consulta de hello toostart, use hello **Execute** botón por debajo de la hoja de cálculo de Hola. Convierte los cambios de texto hello y naranja demasiado**detener**.

3. Cuando haya finalizado la consulta de hello, Hola **resultados** ficha muestra resultados de Hola de operación de Hola. Hola después de texto es resultado de hello de consulta de hello:

        sev       cnt
        [ERROR]   3

    Hola **registros** ficha puede ser información de registro de hello tooview usado creada por el trabajo de Hola.

   > [!TIP]
   > Hola **guardar resultados** cuadro de diálogo de lista desplegable de hello superior izquierda de hello **resultados del proceso de consulta** sección permite toodownload o guardar los resultados.

4. Seleccione Hola cuatro primeras líneas de esta consulta, a continuación, seleccione **Execute**. Tenga en cuenta que no hay ningún resultado, cuando se completa el trabajo de Hola. Con hello **Execute** botón si forma parte de la consulta de hello está activada solamente se ejecuta Hola instrucciones seleccionadas. En este caso, selección de Hola no incluyó la instrucción final Hola que recupera filas de tabla de Hola. Si selecciona sólo esa línea y usar **Execute**, debería ver los resultados de hello esperado.

5. tooadd una hoja de cálculo, use hello **nueva hoja de cálculo** situado en la parte inferior de Hola de hello **Editor de consultas**. En hello nueva hoja de cálculo, escriba Hola siguiendo las instrucciones de HiveQL:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Estas instrucciones realizan Hola siguientes acciones:

   * **CREATE TABLE IF NOT EXISTS** : crea una tabla, si todavía no existe. Desde hello **externo** no se utiliza la palabra clave, se crea una tabla interna. Una tabla interna se almacena en el almacén de datos de Hive de Hola y se administra completamente por el subárbol. A diferencia de las tablas externas, al quitar una tabla interna, eliminan datos subyacente de saludo.

   * **ALMACENA AS ORC** -almacena los datos de hello en formato optimizado fila columnas (ORC). ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.

   * **INSERT OVERWRITE ... Seleccione** -selecciona las filas de hello **log4jLogs** tabla que contenga `[ERROR]`, y, a continuación, inserta Hola datos en hello **registros de errores de** tabla.

     Hola de uso **Execute** botón toorun esta consulta. Hola **resultados** ficha no contiene ninguna información cuando Hola consulta devuelve cero filas. Hola estado debe aparecer como **correcto** cuando consulta Hola se haya completado.

### <a name="visual-explain"></a>Explicación visual

toodisplay una visualización del plan de consulta de hello, seleccione hello **explican Visual** ficha debajo de la hoja de cálculo de Hola.

Hola **explican Visual** la vista de consulta de hello puede ser útil para comprender el flujo de Hola de consultas complejas. Puede ver un equivalente textual de esta vista mediante hello **explicativo** botón Hola Editor de consultas.

### <a name="tez-ui"></a>Interfaz de usuario de Tez

toodisplay Hola Tez UI para consulta de hello, seleccione hello **Tez** ficha debajo de la hoja de cálculo de Hola.

> [!IMPORTANT]
> Tez es tooresolve no se utiliza en todas las consultas. Muchas consultas pueden resolverse sin necesidad de usar Tez. 

Si Tez estuviera consulta de hello tooresolve usado, Hola se muestra el gráfico acíclico dirigido (DAG). Si desea tooview Hola DAG para las consultas que ha ejecutado Hola anteriores o depurar Hola Tez proceso, use hello [Tez vista](hdinsight-debug-ambari-tez-view.md) en su lugar.

## <a name="view-job-history"></a>Visualización del historial de trabajos

Hola __trabajos__ ficha muestra un historial de consultas de Hive.

![Imagen del historial de trabajos de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Tablas de la base de datos

Puede usar hello __tablas__ ficha toowork con tablas en una base de datos de Hive.

![Imagen de la pestaña de tablas de Hola](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Consultas guardadas

Desde la pestaña de consulta de hello, si lo desea puede guardar consultas. Una vez guardado, puede volver a usar consultas de Hola de hello __consultas guardadas__ ficha.

![Imagen de la pestaña de consultas guardadas](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Funciones definidas por el usuario

Hive también puede extenderse a través de funciones definidas por el usuario (UDF). Una UDF permite la funcionalidad de tooimplement o lógica que no está modelada fácilmente en HiveQL.

Hola pestaña UDF en parte superior de Hola de hello Hive vista permite toodeclare y guardar un conjunto de archivos UDF. Estos archivos UDF se pueden utilizar con hello **Editor de consultas**.

![Imagen de la pestaña UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

Una vez haya agregado una vista de Hive, de UDF toohello una **insertar UDF** botón aparece en la parte inferior de Hola de Hola **Editor de consultas**. Al seleccionar esta entrada, muestra una lista de desplegable de hello UDF definidas en hello Hive vista. Si selecciona una UDF, agrega HiveQL instrucciones tooyour consulta tooenable Hola UDF.

Por ejemplo, si ha definido una UDF con hello propiedades siguientes:

* Nombre de recurso: myudfs

* Ruta de acceso de recurso: /myudfs.jar

* Nombre de la UDF: myawesomeudf

* Nombre de la clase UDF: com.myudfs.Awesome

Con hello **insertar UDF** botón muestra una entrada denominada **myudfs**, con otra lista desplegable para cada UDF definidas para ese recurso. En este caso, **myawesomeudf**. Si selecciona esta entrada, agrega Hola después toohello a partir de consultas de hello:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

A continuación, puede usar Hola UDF en la consulta. Por ejemplo: `SELECT myawesomeudf(name) FROM people;`.

Para obtener más información sobre el uso de UDF con Hive en HDInsight, vea Hola siguientes documentos:

* [Uso de Python con Hive y Pig en HDInsight](hdinsight-python.md)
* [¿Cómo tooadd un tooHDInsight Hive UDF personalizado](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Configuración de Hive

La configuración puede ser usado toochange distintas configuraciones de Hive. Por ejemplo, cambiar el motor de ejecución de Hola de Hive de tooMapReduce Tez (valor predeterminado de hello).

## <a id="nextsteps"></a>Pasos siguientes

Para obtener información general acerca de Hive en HDInsight:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)

Para obtener información sobre otras formas en que puede trabajar con Hadoop en HDInsight:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)
