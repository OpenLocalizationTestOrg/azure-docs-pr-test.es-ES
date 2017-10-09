---
title: "Kit de herramientas de Azure para IntelliJ: creación de aplicaciones Spark para un clúster de HDInsight | Microsoft Docs"
description: "Hola de usar el Kit de herramientas de Azure para IntelliJ toodevelop inspirará las aplicaciones escritas en Scala y enviarlos tooan clúster de HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Usar el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de un clúster de HDInsight

Use Hola Kit de herramientas de Azure para aplicaciones de Spark de complemento toodevelop IntelliJ escritas en Scala y, a continuación, envíelos tooan clúster de HDInsight Spark directamente desde el entorno de desarrollo integrado de hello IntelliJ (IDE). Puede usar Hola complemento de varias maneras:

* Desarrollar y enviar una aplicación Spark en Scala en un clúster de Spark en HDInsight.
* Tener acceso a los recursos del clúster de Azure HDInsight Spark.
* Desarrollar y ejecutar localmente una aplicación Spark en Scala.

toocreate su proyecto, Hola vista [crear aplicaciones de Spark con hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) vídeo.

> [!IMPORTANT]
> Puede usar este complemento toocreate y enviar solicitudes para un clúster de HDInsight Spark en Linux.
> 

## <a name="prerequisites"></a>Requisitos previos

- Un clúster Apache Spark en HDInsight Linux. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).
- Kit de desarrollo de Oracle Java. Puede instalarlo desde hello [sitio Web de Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. En este artículo se usa la versión 2017.1. Puede instalarlo desde hello [sitio Web de JetBrains](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Instalación del kit de herramientas de Azure para IntelliJ
Para obtener instrucciones de instalación, consulte [Instalación del kit de herramientas de Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Inicie sesión en tooyour suscripción de Azure

1. Iniciar hello IntelliJ IDE y abra el Explorador de Azure. En hello **vista** menú, seleccione **las ventanas de herramientas**y, a continuación, seleccione **explorador Azure**.
       
   ![vínculo de explorador Azure Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Menú contextual hello **Azure** nodo y, a continuación, seleccione **inicio de sesión**.

3. Hola **inicio de sesión en Azure** cuadro de diálogo, seleccione **iniciar sesión en**y, a continuación, escriba sus credenciales de Azure.

    ![cuadro de Hello Azure inicio de sesión de diálogo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Después de que ha iniciado sesión, Hola **seleccione suscripciones** Hola a todos Hola suscripciones de Azure que están asociadas con el cuadro de diálogo enumera las credenciales. Seleccione hello **seleccione** botón.

    ![cuadro de diálogo Seleccionar suscripciones Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. En hello **explorador Azure** , expanda **HDInsight** tooview Hola clústeres de HDInsight Spark y que se encuentran en su suscripción.
   
    ![Clústeres de HDInsight Spark en Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview Hola recursos (por ejemplo, cuentas de almacenamiento) que están asociados con el clúster de hello, expandir un nodo de nombre del clúster.
   
    ![Nodo de nombre de clúster expandido](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Ejecución de una aplicación Spark en Scala en un clúster de HDInsight Spark

1. Inicie IntelliJ IDEA y, después, cree un proyecto. Hola **nuevo proyecto** diálogo cuadro, Hola siguientes: 

   a. Seleccione **HDInsight** > **Spark en HDInsight (Scala)**.

   b. Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:

      * **Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala
      * **SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola

    ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Seleccione **Siguiente**.

3. Asistente para la creación del proyecto de Hello Scala detecta automáticamente si ha instalado Hola Scala complemento. Seleccione **Instalar**.

   ![Comprobación de complemento de Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Hola toodownload Scala complemento, seleccione **Aceptar**. Siga las instrucciones de hello toorestart IntelliJ. 

   ![cuadro de diálogo de instalación de complemento de Hello Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. Hola **nuevo proyecto** ventana, Hola siguientes:  

    ![Seleccionar Hola Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Escriba un nombre y una ubicación de proyecto.

   b. Hola **proyecto SDK** lista desplegable, seleccione **Java 1.8** para clúster de hello Spark 2.x, o bien seleccione **Java 1.7** para clúster de hello Spark 1.x.

   c. Hola **versión Spark** lista desplegable, el Asistente para crear un proyecto Scala integra con la versión adecuada de Hola de SDK de Spark y Scala SDK. Si la versión de clúster de Spark hello es anterior a la 2.0, seleccione **inspirará 1.x**. De lo contrario, seleccione **Spark 2.x**. Este ejemplo utiliza **Spark 2.0.2 (Scala 2.11.8)**.

6. Seleccione **Finalizar**.

7. proyecto de Spark Hola crea automáticamente un artefacto por usted. artefacto de hello tooview, Hola siguientes:

   a. En hello **archivo** menú, seleccione **estructura del proyecto**.

   b. Hola **estructura del proyecto** cuadro de diálogo, seleccione **artefactos** artefacto de predeterminado de hello tooview que se crea. También puede crear su propios artefacto seleccionando el signo más hello (**+**).

      ![Información de artefacto en el cuadro de diálogo de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Agregue el código fuente de aplicación haciendo Hola siguiente:

   a. En el Explorador de proyectos, haga clic en **src**, seleccione demasiado**New**y, a continuación, seleccione **Scala clase**.
      
      ![Comandos para crear una clase Scala desde el explorador de proyectos](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. Hola **crear nueva clase Scala** diálogo cuadro, proporcione un nombre, seleccione **objeto** en hello **tipo** cuadro y, a continuación, seleccione **Aceptar**.
      
      ![Creación de un cuadro de diálogo de nueva clase de Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. Hola **MyClusterApp.scala** de archivo, pegue el siguiente código de hello. Hello código lee los datos de Hola de HVAC.csv (disponible en todos los clústeres de HDInsight Spark), se recuperan las filas de Hola que sólo tienen un dígito en la columna séptimo hello en el archivo CSV de Hola y escribe la salida de hello demasiado**/HVACOut** en el valor predeterminado de Hola contenedor de almacenamiento de clúster de Hola.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Ejecutar la aplicación hello en un clúster de HDInsight Spark haciendo Hola siguiente:

   a. En el Explorador de proyectos, haga clic en el nombre del proyecto de Hola y, a continuación, seleccione **tooHDInsight enviar Spark aplicación**.
      
      ![comando de tooHDInsight enviar Spark aplicación Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Se está tooenter solicitada sus credenciales de suscripción de Azure. Hola **Spark envío** cuadro de diálogo, proporcione Hola después de valores y, a continuación, seleccione **enviar**.
      
      * Para **inspirará clústeres (solamente para Linux)**, seleccione Hola clúster de HDInsight Spark en el que desea que toorun la aplicación.

      * Seleccione un artefacto hello IntelliJ proyecto o seleccione uno de la unidad de disco duro de Hola.

      * Hola **nombre de la clase principal** cuadro de puntos suspensivos de hello seleccione (**...** ), seleccione la clase principal de hello en el código fuente de aplicación y, a continuación, seleccione **Aceptar**.

        ![cuadro de diálogo Seleccionar clase de Main Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Porque no requiere argumentos de línea de comandos o no hacer referencia a archivos JAR o archivos de código de la aplicación hello en este ejemplo, puede dejar Hola restantes cuadros vacíos. Después de proporcionar toda la información de hello, cuadro de diálogo de hello debe ser similar a Hola después de la imagen.
        
        ![cuadro de diálogo de envío de Spark Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Hola **Spark envío** ficha situada en la parte inferior de Hola de ventana hello debe comenzar a mostrar el progreso de Hola. También puede detener la aplicación hello seleccionando botón rojo Hola Hola **Spark envío** ventana.
      
      ![ventana de envío de Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn cómo tooaccess Hola salida del trabajo, vea Hola "acceso y administrar clústeres de HDInsight Spark mediante el Kit de herramientas de Azure para IntelliJ" sección más adelante en este artículo.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Ejecución o depuración de una aplicación Spark en Scala en un clúster de HDInsight Spark
También se recomienda otra forma de enviar el clúster de hello Spark application toohello. Puede hacerlo estableciendo los parámetros de Hola Hola **las configuraciones de ejecución y depuración** IDE. Para obtener más información, consulte [Depuración de aplicaciones de Spark de forma remota en un clúster de HDInsight con el kit de herramientas de Azure para IntelliJ mediante SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Acceso y administración de clústeres de HDInsight Spark mediante el uso del kit de herramientas de Azure para IntelliJ
Puede realizar varias operaciones mediante el Kit de herramientas de Azure para IntelliJ.

### <a name="access-hello-job-view"></a>Vista de trabajos de Hola de acceso
1. En el Explorador de Azure, expanda **HDInsight**, expanda el nombre del clúster de Spark hello y, a continuación, seleccione **trabajos**.  

    ![Nodo Vista de trabajos](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. En el panel derecho de hello, Hola **Spark trabajo vista** ficha muestra todas las aplicaciones de Hola que se ejecutaron en clúster de Hola. Seleccione el nombre de Hola de aplicación hello para el que desea toosee más detalles.

    ![Detalles de aplicación](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay ejecución trabajo información básica, mantenga el mouse sobre el gráfico de trabajo de Hola. gráfico de fases de hello tooview y la información que genera cada trabajo, seleccione un nodo en el gráfico de trabajo de Hola.

    ![Detalles de fase de trabajo](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview utilizados con frecuencia los registros, como *controlador Stderr*, *controlador Stdout*, y *información de directorio*, seleccione hello **registro** ficha.

    ![Detalles del registro](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. También puede ver Hola historial Spark interfaz de usuario y hello YARN interfaz de usuario (en el nivel de aplicación Hola) seleccionando un vínculo en la parte superior de Hola de ventana hello.

### <a name="access-hello-spark-history-server"></a>Servidor de acceso Hola Spark historial
1. En Azure Explorer, expanda **HDInsight**, haga clic con el botón derecho en el nombre del clúster de Spark y seleccione **Open Spark History UI** (Abrir IU de historial de Spark). 

2. Cuando se le pida, escriba credenciales de administrador del clúster de hello, que especificó al configurar el clúster de Hola.

3. En el panel del servidor de hello Spark historial, puede usar toolook de nombre de aplicación Hola para aplicación Hola que simplemente terminado de ejecutarse. En el anterior código de hello, establecer nombre de la aplicación hello mediante `val conf = new SparkConf().setAppName("MyClusterApp")`. Por lo tanto, el nombre de aplicación Spark es **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Iniciar hello Ambari portal
1. En Azure Explorer, expanda **HDInsight**, haga clic con el botón derecho en el nombre del clúster de Spark y seleccione **Open Cluster Management Portal (Ambari)** (Abrir el portal de administración de clústeres [Ambari]). 

2. Cuando se le pida, escriba las credenciales de administrador de hello para el clúster de Hola. Estas credenciales se especificó durante el proceso de instalación de clúster de Hola.

### <a name="manage-azure-subscriptions"></a>Administración de suscripciones de Azure
De forma predeterminada, Azure Toolkit for IntelliJ enumera los clústeres de Spark Hola de todas las suscripciones de Azure. Si es necesario, puede especificar las suscripciones de Hola que desea tooaccess. 

1. En el Explorador de Azure, haga clic en hello **Azure** nodo raíz y, a continuación, seleccione **administrar suscripciones**. 

2. En el cuadro de diálogo de hello, desactive Hola casillas de verificación siguiente toohello las suscripciones que no desee tooaccess y, a continuación, seleccione **cerrar**. También puede seleccionar **cerrar sesión** si desea toosign fuera de su suscripción de Azure.

## <a name="run-a-spark-scala-application-locally"></a>Ejecución local de una aplicación Spark en Scala
Puede usar el Kit de herramientas de Azure para aplicaciones de IntelliJ toorun Spark Scala localmente en la estación de trabajo. Hola aplicaciones normalmente no necesita tener acceso a recursos de toocluster, como contenedores de almacenamiento, y se puede ejecutar y se prueban localmente.

### <a name="prerequisite"></a>Requisito previo
Mientras se ejecuta la aplicación local de Spark Scala de hello en un equipo Windows, podría obtener una excepción, como se explica en [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). excepción de Hola se produce porque falta WinUtils.exe en Windows. 

tooresolve este error, [descargar ejecutable hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa ubicación como **C:\WinUtils\bin**. A continuación, agregue la variable de entorno de hello **HADOOP_HOME**y establezca el valor de Hola de variable de hello demasiado**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Ejecución de una aplicación Spark en Scala local
1. Inicie IntelliJ IDEA y cree un proyecto. 

2. Hola **nuevo proyecto** diálogo cuadro, Hola siguientes:
   
    a. Seleccione **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Ejemplo de ejecución local de Spark en HDInsight [Scala]).

    b. Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:

      * **Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala
      * **SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola

    ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Seleccione **Siguiente**.
 
4. En la siguiente ventana de Hola Hola siguientes:
   
    a. Escriba un nombre y una ubicación de proyecto.

    b. Hola **proyecto SDK** lista desplegable, seleccione una versión de Java que es posterior a la versión 1.7.

    c. Hola **versión Spark** lista desplegable, versión de Hola select de Scala que desea toouse: Scala 2.11.x para Spark 2.0 o Scala 2.10.x para Spark 1.6.

    ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Seleccione **Finalizar**.

6. plantilla de Hello agrega un código de ejemplo (**LogQuery**) en hello **src** carpeta que puede ejecutar localmente en el equipo.
   
    ![Ubicación de LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Menú contextual hello **LogQuery** aplicación y, a continuación, seleccione **ejecución 'LogQuery'**. En hello **ejecutar** ficha en la parte inferior de hello, verá una salida como Hola siguiente:
   
   ![Resultado de la ejecución local de la aplicación Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Convertir existente IntelliJ IDEA aplicaciones toouse Kit de herramientas de Azure para IntelliJ
Puede convertir Hola Spark Scala las aplicaciones existentes que ha creado en la IDEA de IntelliJ toobe compatible con el Kit de herramientas de Azure para IntelliJ. A continuación, puede usar hello toosubmit complemento Hola aplicaciones tooan clúster de HDInsight Spark.

1. Para una aplicación de Spark Scala existente que se creó a través de la IDEA de IntelliJ, abra el archivo de .iml asociados de Hola.

2. En la raíz de hello nivel es un **módulo** elemento como Hola siguiente:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Editar Hola elemento tooadd `UniqueKey="HDInsightTool"` así que Hola **módulo** elemento aspecto Hola siguiente:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Guarde los cambios de Hola. La aplicación ahora debe ser compatible con el kit de herramientas de Azure para IntelliJ. Se puede probar haciendo clic en el nombre del proyecto hello en el Explorador de proyectos. menú emergente de Hello ahora tiene la opción de hello **tooHDInsight enviar Spark aplicación**.

## <a name="troubleshooting"></a>Solución de problemas

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Error en la ejecución local: *Please use a larger heap size* (Utilice un tamaño de montón mayor)
En Spark 1.6, si usas un SDK de Java de 32 bits durante la ejecución local, podría encontrar Hola siguientes errores:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Estos errores tienen lugar porque el tamaño del montón de hello no es lo suficientemente grande como para toorun Spark. Spark requiere al menos 471 MB. (para obtener más información, consulte [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081)). Una solución simple es toouse un SDK de Java de 64 bits. También puede cambiar la configuración de JVM hello en IntelliJ agregando Hola siguientes opciones:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Agregar opciones toohello "Opciones de VM" cuadro IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>P+F
elegir un almacén de aplicación tooAzure Data Lake, toosubmit **Interactive** modo durante el proceso de Hola de inicio de sesión Azure. Si selecciona el modo **Automatizado**, puede aparecer un error.

![inicio de sesión interactivo](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

Ahora se ha resuelto. Puede elegir la aplicación de un clúster de Azure datos Lake toosubmit con cualquier método de inicio de sesión.

## <a name="feedback-and-known-issues"></a>Comentarios y problemas conocidos
Actualmente, la visualización de salidas de Spark directamente no se admite.

Si tiene sugerencias o comentarios, o si se le presenta algún problema al usar este complemento, no dude en enviarnos un correo electrónico a la dirección hdivstool@microsoft.com.

## <a name="seealso"></a>Pasos siguientes
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demostración
* Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)
* Depuración remota (vídeo): [Use Azure Toolkit IntelliJ toodebug Spark para aplicaciones de forma remota en clúster de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Escenarios
* [Spark con BI: realización del análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con aprendizaje automático: Use Spark en tooanalyze HDInsight generar temperatura utilizando los datos HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [La transmisión por secuencias Spark: Use Spark en HDInsight toobuild aplicaciones de transmisión por secuencias en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el Kit de herramientas de Azure para las aplicaciones de IntelliJ toodebug Spark forma remota a través de VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar el Kit de herramientas de Azure para aplicaciones de Spark IntelliJ toodebug forma remota a través de SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

