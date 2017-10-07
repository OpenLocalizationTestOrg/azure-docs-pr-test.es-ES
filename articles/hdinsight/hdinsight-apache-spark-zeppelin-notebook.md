---
title: "clúster de blocs de notas de aaaUse Zeppeling con Apache Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Instrucciones paso a paso sobre cómo se agrupa los blocs de notas de toouse Zeppeling con Apache Spark en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Uso de cuadernos de Zeppelin con un clúster Apache Spark en Azure HDInsight

Clústeres de HDInsight Spark incluyen blocs de notas de Zeppeling que puede usar los trabajos de Spark toorun. En este artículo, aprenderá cómo toouse Hola Bloc de notas de Zeppeling en un clúster de HDInsight.

> [!NOTE]
> Los notebooks de Zeppelin están disponibles solo para Spark 1.6.3 en HDInsight 3.5 y Spark 2.1.0 en HDInsight 3.6.
>

**Requisitos previos:**

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Inicio de un cuaderno de Zeppelin Notebook
1. En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Bloc de notas de Zeppeling**. Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.
   
   > [!NOTE]
   > También puede tener acceso a hello Zeppeling Bloc de notas para el clúster por abrir Hola siguiente dirección URL en el explorador. Reemplace **CLUSTERNAME** con nombre hello del clúster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Cree un nuevo notebook. En el panel de encabezado de hello, haga clic en **Bloc de notas**y, a continuación, haga clic en **crear nueva nota**.
   
    ![Creación de un nuevo cuaderno de Zeppeling](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Creación de un nuevo cuaderno de Zeppeling")
   
    Escriba un nombre para el Bloc de notas de hello y, a continuación, haga clic en **crear nota**.
3. Asegúrese también de que el encabezado de Bloc de notas de hello muestra un estado conectado. Se indica mediante un punto verde en la esquina superior derecha de Hola.
   
    ![Estado del cuaderno de Zeppeling](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Estado del cuaderno de Zeppeling")
4. Cargue los datos de ejemplo en una tabla temporal. Cuando se crea un clúster de Spark en HDInsight, archivo de datos de ejemplo de Hola, **hvac.csv**, es copiada toohello asociado de cuenta de almacenamiento en **\HdiSamples\SensorSampleData\hvac**.
   
    En que se crea de forma predeterminada en Bloc de notas nuevo Hola párrafo vacío de hello, pegue Hola siguiente fragmento de código.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Presione **MAYÚS + ENTRAR** o haga clic en hello **reproducir** botón para el fragmento de código de hello párrafo toorun Hola. estado de Hello en la esquina derecha de Hola de párrafo Hola debe avanzan desde que se esté listo, pendiente, tooFINISHED de ejecución. salida de Hello aparezca en parte inferior de Hola de hello mismo párrafo. captura de pantalla de Hello es similar a Hola siguiente:
   
    ![Creación de una tabla temporal a partir de datos sin procesar](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Creación de una tabla temporal a partir de datos sin procesar")
   
    También puede proporcionar un párrafo de tooeach de título. En la esquina derecha de hello, haga clic en hello **configuración** icono y, a continuación, haga clic en **Mostrar título**.
5. Ahora puede ejecutar instrucciones SQL de Spark en hello **hvac** tabla. Pegue Hola después de consulta en un párrafo nuevo. consulta de Hello recupera el identificador de edificio de Hola y diferenciar hello en destino hello y temperaturas reales de cada edificio, en una fecha determinada. Presione **MAYÚS + ENTRAR**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Hola **% sql** instrucción al principio de hello indica Livio Scala intérprete de hello Bloc de notas toouse Hola.
   
    Hello captura de pantalla siguiente muestra el resultado de hello.
   
    ![Ejecutar una instrucción de Spark SQL mediante el Bloc de notas de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "ejecutar una instrucción de Spark SQL mediante el Bloc de notas de Hola")
   
     Haga clic en hello Mostrar opciones (resaltado en el rectángulo) tooswitch entre diferentes representaciones de hello mismo resultado. Haga clic en **configuración** toochoose qué constituye Hola clave y valores de salida de hello. Hola captura de pantalla anterior se usa **buildingID** como clave de Hola y promedio de Hola de **temp_diff** como valor de Hola.
6. También puede ejecutar instrucciones SQL de Spark mediante variables de consulta de Hola. Hola fragmento de código siguiente se muestra cómo toodefine una variable, **Temp**, en la consulta de hello cuyos valores posibles son Hola desea tooquery con. Cuando ejecuta consultas de Hola por primera vez, una lista desplegable se rellena automáticamente con valores de hello especificados para la variable de saludo.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    Pegue este fragmento de código en un nuevo párrafo y presione **MAYÚS + ENTRAR**. Hello captura de pantalla siguiente muestra el resultado de hello.
   
    ![Ejecutar una instrucción de Spark SQL mediante el Bloc de notas de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "ejecutar una instrucción de Spark SQL mediante el Bloc de notas de Hola")
   
    Para las consultas posteriores, puede seleccionar un nuevo valor de lista desplegable de Hola y vuelva a ejecutar consulta Hola. Haga clic en **configuración** toochoose qué constituye Hola clave y valores de salida de hello. Hola captura de pantalla anterior se usa **buildingID** como clave de hello, Hola promedio de **temp_diff** como valor de hello, y **targettemp** como grupo de Hola.
7. Reinicie la aplicación hello de Livio intérprete tooexit Hola. toodo, abra Configuración de intérprete haciendo clic en hello registra en nombre de usuario desde la esquina superior derecha de hello y, a continuación, haga clic en **intérprete**.
   
    ![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")
8. Desplácese tooLivy configuración de intérprete y, a continuación, haga clic en **reiniciar**.
   
    ![Reinicie Hola Livio intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar hello Zeppeling intepreter")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>¿Cómo se puede usar los paquetes externos con el Bloc de notas de Hola?
Puede configurar el Bloc de notas de hello Zeppeling en clústeres de Apache Spark en HDInsight (Linux) toouse externos, contribuyeron a la Comunidad de paquetes que no se incluye fuera-de-predeterminada en clúster de Hola. Puede buscar hello [repositorio Maven](http://search.maven.org/) para la lista completa de Hola de paquetes que están disponibles. También puede obtener una lista de paquetes disponibles de otras fuentes. Por ejemplo, dispone de la lista completa de los paquetes externos aportados por la comunidad en [Spark Packages](http://spark-packages.org/)(Paquetes Spark).

En este artículo, verá cómo hello toouse [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paquete con el Bloc de notas de hello Jupyter.

1. Abra la configuración del intérprete. Desde la esquina superior derecha de hello, haga clic en hello registrado en nombre de usuario y, a continuación, haga clic en **intérprete**.
   
    ![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")
2. Desplácese tooLivy configuración de intérprete y, a continuación, haga clic en **editar**.
   
    ![Cambio de la configuración del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Cambio de la configuración del intérprete")
3. Agregue una nueva clave denominada **livy.spark.jars.packages** y establezca su valor en formato de hello `group:id:version`. Por lo tanto, si desea hello toouse [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paquete, debe establecer valor de Hola de clave de hello demasiado`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Cambio de la configuración del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Cambio de la configuración del intérprete")
   
    Haga clic en **guardar** y, a continuación, reinicie Hola intérprete Livio.
4. **Sugerencia**: si desea que toounderstand forma de especificar tooarrive como valor de Hola de clave de hello anteriormente, a continuación cómo.
   
    a. Busque el paquete de Hola Hola Maven repositorio. En este tutorial, hemos utilizado [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Repositorio de hello, recopilar los valores de hello de **GroupId**, **ArtifactId**, y **versión**.
   
    ![Uso de paquetes externos con cuadernos de Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Uso de paquetes externos con cuadernos de Jupyter")
   
    c. Concatenar valores de hello tres, separados por dos puntos (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>¿Dónde está Hola blocs de notas Zeppeling guardados?
blocs de notas de Hello Zeppeling se guardan toohello headnodes de clúster. Por lo tanto, si elimina el clúster de hello, blocs de notas de Hola se eliminarán también. Si desea toopreserve los blocs de notas para su uso posterior en otros clústeres, debe exportar cuando haya terminado de ejecutar trabajos de Hola. tooexport un bloc de notas, haga clic en hello **exportar** icono tal y como se muestra en la imagen de hello siguiente.

![Descargar el Bloc de notas](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Bloc de notas de Hola de descarga")

Esto ahorra Bloc de notas de Hola como un archivo JSON en la ubicación de descarga.

## <a name="livy-session-management"></a>Administración de sesiones de Livy
Cuando se ejecuta el primer párrafo de código de hello en el Bloc de notas Zeppeling, se crea una nueva sesión Livio en el clúster de HDInsight Spark. Esta sesión se compartirá con todos los cuadernos de Zeppelin Notebook que cree en el futuro. If para algunos hello motivo Livio sesión es eliminado (reinicio de clúster, etc.), no será capaz de toorun trabajos desde el Bloc de notas de hello Zeppeling.

En tal caso, debe realizar Hola siguiendo los pasos antes de empezar a ejecutar trabajos de un bloc de notas de Zeppeling. 

1. Reinicie Hola intérprete Livio desde el Bloc de notas de hello Zeppeling. toodo, abra Configuración de intérprete haciendo clic en hello registra en nombre de usuario desde la esquina superior derecha de hello y, a continuación, haga clic en **intérprete**.
   
    ![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")
2. Desplácese tooLivy configuración de intérprete y, a continuación, haga clic en **reiniciar**.
   
    ![Reinicie Hola Livio intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar hello Zeppeling intepreter")
3. Ejecute una celda de código desde el cuaderno de Zeppelin Notebook existente. Esto crea una nueva sesión de Livio en clúster de HDInsight Hola.

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
* [Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







