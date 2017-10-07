---
title: "datos de tooanalyze Apache Spark en almacén de Azure Data Lake aaaUse | Documentos de Microsoft"
description: "Ejecutar trabajos de Spark tooanalyze los datos almacenados en el almacén de Azure Data Lake"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Usar datos de tooanalyze de clúster de HDInsight Spark en almacén de Data Lake

En este tutorial, utilizará Jupyter notebook disponible con clústeres de HDInsight Spark toorun un trabajo que lee los datos de una cuenta de almacén de Data Lake.

## <a name="prerequisites"></a>Requisitos previos

* Cuenta de Azure Data Lake Store. Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).

* Clúster de Azure HDInsight Spark con Data Lake Store como almacenamiento. Siga las instrucciones de hello en [crear un clúster de HDInsight con el almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Preparar los datos de Hola

> [!NOTE]
> No es necesario tooperform en este paso si ha creado el clúster de HDInsight de hello con almacén de Data Lake como almacenamiento predeterminado. procesos de creación de clúster de Hello agrega algunos datos de ejemplo en la cuenta de almacén de Data Lake Hola que especifique al crear el clúster de Hola. Omitir la sección toohello [clúster Use HDInsight Spark con almacén de Data Lake](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

Si ha creado un clúster de HDInsight con el almacén de Data Lake como almacenamiento adicional y Blob de almacenamiento de Azure como almacenamiento predeterminado, primero debe copiar sobre algunos toohello de datos de ejemplo cuenta de almacén de Data Lake. Puede usar datos de ejemplo de Hola de hello que BLOB de almacenamiento de Azure asociado con el clúster de HDInsight Hola. Puede usar hello [ADLCopy herramienta](http://aka.ms/downloadadlcopy) toodo para. Descargue e instale la herramienta de Hola desde el vínculo de Hola.

1. Abra un símbolo del sistema y desplácese directorio toohello AdlCopy está instalado, por lo general `%HOMEPATH%\Documents\adlcopy`.

2. Ejecute hello después comando toocopy un blob en cuestión desde Hola origen contenedor tooa almacén de Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Hola copia **HVAC.csv** archivo de datos de ejemplo de **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello cuenta de almacén de Azure Data Lake. fragmento de código de Hello debería ser similar:

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Asegúrese de que Hola archivo y nombres de ruta de acceso están en mayúsculas o minúsculas Hola.
   >
   >
3. Podrá tooenter solicitada credenciales Hola para Hola suscripción de Azure en la que dispone de su cuenta de almacén de Data Lake. Verá un siguiente toohello similar de salida:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    archivo de datos de Hello (**HVAC.csv**) se copiarán en una carpeta **/hvac** Hola cuenta de almacén de Data Lake.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Uso de un clúster de HDInsight Spark con Data Lake Store

1. De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.

2. En la hoja de clúster de Spark hello, haga clic en **vínculos rápidos**y, a continuación, desde hello **panel clúster** hoja, haga clic en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.

   > [!NOTE]
   > También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Cree un nuevo notebook. Haga clic en **Nuevo** y, luego, en **PySpark**.

    ![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Crear un nuevo cuaderno de Jupyter")

4. Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente. contextos de Spark y Hive Hola se crearán automáticamente automáticamente cuando se ejecuta la primera celda de código de hello. Puede iniciar mediante la importación de tipos de hello necesarios para este escenario. toodo por lo tanto, pegue Hola siguiente fragmento de código en una celda y presione **MAYÚS + ENTRAR**.

        from pyspark.sql.types import *

    Cada vez que ejecute un trabajo en Jupyter, el título de ventana del explorador web le mostrará un **(estado ocupado)** estado junto con el título de hello Bloc de notas. También verá un toohello siguiente círculo sólido **PySpark** texto en la esquina superior derecha de Hola. Una vez completado el trabajo de hello, esto también cambiará círculo hueco tooa.

     ![Estado de un trabajo de cuaderno de Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Estado de un trabajo de cuaderno de Jupyter")

5. Cargar datos de ejemplo en una tabla temporal con hello **HVAC.csv** archivo copiado toohello cuenta de almacén de Data Lake. Puede tener acceso a datos de hello en la cuenta de almacén de Data Lake de hello mediante Hola siguiendo el modelo de dirección URL.

    * Si dispone de almacén de Data Lake como almacenamiento predeterminado, HVAC.csv estará en toohello similar en la ruta de acceso de hello después de la dirección URL:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        O bien, también podría utilizar un formato abreviado como siguiente hello:

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Si dispone de almacén de Data Lake como almacenamiento adicional, HVAC.csv estará en hello ubicación donde haya copiado, como:

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     En una celda vacía, Hola pegar siguiente ejemplo de código, reemplace **MYDATALAKESTORE** con el nombre de la cuenta de almacén de Data Lake y presione **MAYÚS + ENTRAR**. Este ejemplo de código registra datos de hello en una tabla temporal denominada **hvac**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Puesto que está utilizando un núcleo de PySpark, ahora puede ejecutar directamente una consulta SQL en la tabla temporal de Hola **hvac** que acaba de crear mediante el uso de hello `%%sql` magia. Para obtener más información acerca de hello `%%sql` mágico, así como otros magics disponibles con kernel PySpark de hello, consulte [núcleos disponibles en los equipos portátiles Jupyter con clústeres de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. Una vez que se complete correctamente el trabajo de hello, Hola siguiendo la salida tabular se muestra de forma predeterminada.

      ![Salida de tabla del resultado de la consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Salida de tabla del resultado de la consulta")

     También puede ver los resultados de hello en otras visualizaciones. Por ejemplo, un gráfico de áreas para hello misma salida sería Hola siguiente.

     ![Gráfico de área del resultado de la consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gráfico de área del resultado de la consulta")

8. Una vez haya terminado de ejecutar la aplicación hello, debería recursos de hello toorelease de apagado Hola Bloc de notas. toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**. Este se apagará y portátil de hello cerrar.


## <a name="next-steps"></a>Pasos siguientes

* [Crear un toorun de aplicación independiente Scala en clúster de Apache Spark](hdinsight-apache-spark-create-standalone-application.md)
* [Usar herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de clúster de HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar herramientas de HDInsight en el Kit de herramientas de Azure Eclipse toocreate Spark para las aplicaciones de clúster de HDInsight Spark Linux](hdinsight-apache-spark-eclipse-tool-plugin.md)
