---
title: "aaaSpark BI mediante herramientas de visualización de datos en HDInsight de Azure | Documentos de Microsoft"
description: "Uso de herramientas de visualización de datos para análisis con Apache Spark BI en clústeres de HDInsight"
keywords: "Apache Spark BI, Spark BI, visualización de datos de Spark, inteligencia empresarial de Spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Apache Spark BI mediante herramientas de visualización de datos con Azure HDInsight

Obtenga información acerca de la visualización de datos de toouse herramientas como tooanalyze Power BI y Tableau un conjunto de datos de ejemplo sin formato mediante Apache Spark BI en clústeres de HDInsight.

> [!NOTE]
> La conectividad con las herramientas de BI que se describen en este artículo no se admite en la versión 2.1 de Spark de la versión 3.6 preliminar de HDInsight de Azure. Solo las versiones de Spark 1.6 y 2.0 (3.4 y 3.5 de HDInsight respectivamente) son compatibles.
>

Este tutorial también está disponible como un cuaderno de Jupyter Notebook en un clúster Spark de HDInsight. experiencia de Bloc de notas de Hello le permite ejecutar fragmentos de código de Python Hola desde Bloc de notas de hello propio. tutorial de hello tooperform desde dentro de un bloc de notas, cree un clúster de Spark, inicie Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), y, a continuación, ejecutar el Bloc de notas de hello **herramientas de BI de uso con Apache Spark en HDInsight.ipynb** en hello **Python**  carpeta.

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Preparación de los datos para la visualización de datos de Spark

En esta sección, se utiliza hello [Jupyter](https://jupyter.org) Bloc de notas de un HDInsight Spark clúster toorun los trabajos que procesan los datos de ejemplo sin formato y guardarla como una tabla. datos de ejemplo de Hola están un archivo .csv (hvac.csv) disponible en todos los clústeres de forma predeterminada. Una vez que los datos se guardan como una tabla, en la sección siguiente de hello es usar la tabla de toohello de tooconnect de herramientas de BI y realicemos visualizaciones de datos.

> [!NOTE]
> Si va a realizar Hola los pasos de este artículo después de completar las instrucciones de hello en [ejecutar las consultas interactivas en un clúster de HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md), puede omitir tooStep 8 siguiente.
>

1. De hello [portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio). También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.   

2. En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Jupyter Notebook**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.

   > [!NOTE]
   > También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Cree un cuaderno. Haga clic en **Nuevo** y, luego, en **PySpark**.

    ![Creación de un cuaderno de Jupyter Notebook para Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Creación de un cuaderno de Jupyter Notebook para Apache Spark BI")

4. Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled.pynb. Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo.

    ![Proporcione un nombre para el Bloc de notas de Hola para Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "proporcione un nombre para el Bloc de notas de Hola para Apache Spark BI")

5. Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente. contextos de Spark y Hive Hola se crean automáticamente cuando se ejecuta la primera celda de código de hello. Puede iniciar mediante la importación de tipos de hello necesarios para este escenario. toodo por lo tanto, coloque cursor de hello en la celda de hello y presione **MAYÚS + ENTRAR**.

        from pyspark.sql import *

6. Cargue los datos de ejemplo en una tabla temporal. Cuando se crea un clúster de Spark en HDInsight, archivo de datos de ejemplo de Hola, **hvac.csv**, es copiada toohello asociado de cuenta de almacenamiento en **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    En una celda vacía, pegue el siguiente Hola fragmento y presione **MAYÚS + ENTRAR**. Este fragmento de código registra datos de hello en una tabla denominada **hvac**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Compruebe que la tabla Hola se creó correctamente. Puede usar hello `%%sql` mágico consultas de Hive toorun directamente. Para obtener más información acerca de hello `%%sql` mágico y otros magics disponibles con kernel PySpark de hello, vea [núcleos disponibles en los equipos portátiles Jupyter con clústeres de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Verá una salida como la que se muestra a continuación:

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Hola solo las tablas que tienen false en hello **isTemporary** columna son tablas de subárbol que se almacenan en la tienda de metadatos de Hola y pueden tener acceso desde herramientas de BI de Hola. En este tutorial, nos conectamos toohello **hvac** tabla hemos creado.

8. Comprobar que esa tabla hello contiene datos de hello prevista. En una celda vacía en el Bloc de notas de hello, copie el siguiente de hello fragmento y presione **MAYÚS + ENTRAR**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Apagar los recursos de Hola de toorelease de hello Bloc de notas. toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.

## <a name="powerbi"></a>Uso de Power BI para la visualización de datos de Spark

> [!NOTE]
> Esta sección se aplica solo a Spark 1.6 en HDInsight 3.4 y Spark 2.0 en HDInsight 3.5.
>
>

Una vez que ha guardado los datos de hello como una tabla, puede usar datos de Power BI tooconnect toohello y visualizar informes toocreate, paneles, etcetera.

1. Asegúrese de que tiene acceso tooPower BI. Puede obtener una suscripción de versión preliminar gratuita de Power BI en [http://www.powerbi.com/](http://www.powerbi.com/).

2. Inicie sesión en demasiado[Power BI](http://www.powerbi.com/).

3. Desde la parte inferior del panel izquierdo de Hola Hola haga clic en **obtener datos**.

4. En hello **obtener datos** página, en **importar o conectarse tooData**, para **bases de datos**, haga clic en **obtener**.

    ![Obtención de datos en Power BI para Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Obtención de datos en Power BI para Apache Spark BI")

5. En la siguiente pantalla de bienvenida, haga clic en **Spark en HDInsight de Azure** y, a continuación, haga clic en **conectar**. Cuando se le solicite, escriba la dirección URL del clúster de hello (`mysparkcluster.azurehdinsight.net`) y Hola credenciales tooconnect toohello clúster.

    ![Conectar tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "conectar tooApache Spark BI")

    Una vez establecida la conexión de hello, Power BI inicia la importación de datos de clúster de hello Spark en HDInsight.

6. Power BI importa los datos de Hola y agrega un **Spark** conjunto de datos en hello **conjuntos de datos** encabezado. Haga clic en el conjunto de datos de hello tooopen una nueva hoja de cálculo toovisualize Hola de datos. También puede guardar la hoja de cálculo de Hola como un informe. una hoja de cálculo de hello toosave **archivo** menú, haga clic en **guardar**.

    ![Icono de Apache Spark BI en el panel de Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Icono de Apache Spark BI en el panel de Power BI")
7. Tenga en cuenta que hello **campos** lista de la derecha de hello muestra hello **hvac** tabla que creó anteriormente. Expanda campos de hello toosee hello de la tabla en la tabla de hello, tal y como se definió anteriormente en el Bloc de notas.

      ![Lista de tablas en el panel de Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Lista de tablas en el panel de Apache Spark BI")

8. Crear una variación de visualización tooshow Hola entre temperatura de destino y la temperatura real para cada compilación. Seleccionar datos de yoru toovisualize, **gráfico de áreas** (que se muestra en el cuadro rojo). eje de hello toodefine, arrastrar y colocar hello **BuildingID** campo **eje**, y **ActualTemp**/**TargetTemp** campos en **valor**.

    ![Creación de visualizaciones de datos de Spark con Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Creación de visualizaciones de datos de Spark con Apache Spark BI")

9. De forma predeterminada visualización Hola muestra la suma de hello para **ActualTemp** y **TargetTemp**. Por tanto Hola los campos de hello lista desplegable, seleccione **Media** tooget un promedio de real y la temperatura de destino para ambos edificios.

    ![Creación de visualizaciones de datos de Spark con Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Creación de visualizaciones de datos de Spark con Apache Spark BI")

10. La visualización de datos debe ser similar toohello uno en la captura de pantalla de Hola. Mueva el cursor sobre Hola visualización tooget información sobre herramientas con datos relevantes.

    ![Creación de visualizaciones de datos de Spark con Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Creación de visualizaciones de datos de Spark con Apache Spark BI")

11. Haga clic en **guardar** de hello principales de menú y proporcione un nombre de informe. También puede anclar Hola visual. Al anclar una visualización, se almacena en el panel por lo que puede controlar los valores más recientes de hello un vistazo.

   Puede agregar tantos visualizaciones como desee para Hola el mismo conjunto de datos y anclarlos toohello panel para una instantánea de los datos. Asimismo, clústeres de Spark en HDInsight son tooPower conectado BI con direct conectarse. Esto asegura que Power BI siempre tiene Hola mayoría de los datos actualizada desde el clúster no es necesario tooschedule actualizaciones para el conjunto de datos de Hola.

## <a name="tableau"></a>Uso de Tableau Desktop para la visualización de datos de Spark

> [!NOTE]
> Esta sección solo es aplicable a los clústeres de Spark 1.5.2 creados en Azure HDInsight.
>
>

1. Instalar [Tableau Desktop](http://www.tableau.com/products/desktop) en equipo Hola donde se ejecuta este tutorial de Apache Spark BI.

2. Asegúrese de que el equipo también tenga instalado el controlador ODBC de Microsoft Spark. Puede instalar controladores de Hola de [aquí](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Inicie Tableau Desktop. En el panel izquierdo de hello, en lista de Hola de tooconnect de servidor, haga clic en **Spark SQL**. Si Spark SQL no aparece de forma predeterminada en el panel izquierdo de hello, puede buscar haciendo clic en **más servidores**.
2. En el cuadro de diálogo de conexión de hello Spark SQL, proporcione los valores de hello tal y como se muestra en la captura de pantalla de hello y, a continuación, haga clic en **Aceptar**.

    ![Clúster de tooa conectar a Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "conectar tooa clústeres de Apache Spark BI")

    Hola listas desplegables de autenticación **servicio HDInsight de Microsoft Azure** como una opción, solo si ha instalado hello [controlador ODBC de Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) en el equipo de Hola.
3. En pantalla siguiente hello, de hello **esquema** lista desplegable, haga clic en hello **buscar** icono y, a continuación, haga clic en **predeterminado**.

    ![Búsqueda del esquema de Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Búsqueda del esquema de Apache Spark BI")
4. Para hello **tabla** , a continuación, haga clic en hello **buscar** icono nuevo toolist Hola a todos Hive tablas disponibles en el clúster de Hola. Debería ver Hola **hvac** tabla creada anteriormente con el Bloc de notas de Hola.

    ![Búsqueda de la tabla de Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Búsqueda de la tabla de Apache Spark BI")
5. Arrastre y coloque el cuadro superior toohello de hello tabla en hello derecho. Tableau importa datos de Hola y muestra el esquema de hello como se resalta cuadro Hola rojo.

    ![Agregar tablas tooTableau para Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "agregar tablas tooTableau para Apache Spark BI")
6. Haga clic en hello **Sheet1** pestaña en hello parte inferior izquierda. Realizar una visualización que muestra destino promedio de Hola y la temperatura real para todos los edificios para cada fecha. Arrastre **fecha** y **Id. de edificio** demasiado**columnas** y **Temp real**/**destino Temp**demasiado**filas**. En **marcas**, seleccione **área** toouse un mapa de área de visualización de datos de Spark.

     ![Incorporación de campos para la visualización de datos de Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Incorporación de campos para la visualización de datos de Spark")
7. De forma predeterminada, se muestran los campos de temperatura de hello como agregado. Si desea que las temperaturas medias de hello tooshow en su lugar, puede hacerlo desde la lista desplegable Hola tal y como se muestra a continuación.

    ![Realización del promedio de temperatura para la visualización de datos de Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Realización del promedio de temperatura para la visualización de datos de Spark")

8. Puede también super-imponer una asignación de temperatura Hola en otro tooget una idea más clara de la diferencia entre el destino y la temperatura real. Mover esquina de hello mouse toohello de asignación de área inferior de hello hasta que vea forma de identificador hello resaltado en un círculo rojo. Arrastre Hola mapa toohello otra asignación de Hola superior y versión Hola mouse cuando vea forma Hola resaltado en el rectángulo rojo.

    ![Combinación de mapas para la visualización de datos de Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Combinación de mapas para la visualización de datos de Spark")

     Como se muestra en la captura de pantalla de hello, debe cambiar la visualización de datos:

    ![Salida de Tableau para la visualización de datos de Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Salida de Tableau para la visualización de datos de Spark")
9. Haga clic en **guardar** hoja de cálculo de toosave Hola. Puede crear paneles y agregar uno o más tooit hojas.

## <a name="next-steps"></a>Pasos siguientes

Hasta ahora, ha aprendido cómo crear Spark marcos tooquery datos toocreate un clúster y, a continuación, tener acceso a esos datos desde herramientas de BI. Ahora puede consultar instrucciones sobre cómo toomanage Hola recursos de clúster y depurar los trabajos que se ejecutan en un clúster de HDInsight Spark.

* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

