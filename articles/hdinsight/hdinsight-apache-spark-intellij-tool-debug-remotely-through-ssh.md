---
title: "Kit de herramientas de Azure para IntelliJ: depuración de aplicaciones Spark de forma remota mediante SSH | Microsoft Docs"
description: "Instrucciones paso a paso sobre cómo toouse herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toodebug para aplicaciones de forma remota en HDInsight clústeres a través de SSH"
keywords: "depurar remotamente intellij, depuración remota intellij, ssh, intellij, hdinsight, depurar intellij, depuración"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Depuración de aplicaciones Spark en un clúster de HDInsight con el Kit de herramientas de Azure para IntelliJ mediante SSH

Este artículo proporciona instrucciones paso a paso acerca de cómo toouse herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toodebug para aplicaciones de forma remota en un clúster de HDInsight. toodebug el proyecto, también puede ver hello [aplicaciones depurar HDInsight Spark con el Kit de herramientas de Azure para IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) vídeo.

**Requisitos previos**

* **Herramientas de HDInsight del kit de herramientas de Azure para IntelliJ**. Esta herramienta es parte del Kit de herramientas de Azure para IntelliJ. Para más información, vea [Instalación del kit de herramientas de Azure para IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Kit de herramientas de Azure para IntelliJ**. Use esta aplicación de Spark toocreate Kit de herramientas para un clúster de HDInsight. Para obtener más información, siga las instrucciones de hello en [Use Azure Toolkit IntelliJ toocreate Spark para las aplicaciones de un clúster de HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **Servicio SSH de HDInsight con administración de nombre de usuario y contraseña**. Para obtener más información, consulte [conectar tooHDInsight (Hadoop) a través de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y [utilizar SSH túneles tooaccess Ambari web UI, JobHistory, NameNode, Oozie y otras interfaces de usuario web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Creación de una aplicación Scala de Spark y configuración para la depuración remota

1. Inicie IntelliJ IDEA y, después, cree un proyecto. Hola **nuevo proyecto** diálogo cuadro, Hola siguientes:

   a. Seleccione **HDInsight**. 

   b. Seleccione una plantilla de Java o Scala según sus preferencias. Seleccione entre Hola siguientes opciones:

      - **Spark en HDInsight (Scala)**

      - **Spark en HDInsight (Java)**

      - **Spark en el ejemplo de ejecución de clúster de HDInsight (Scala)**

      En este ejemplo se usa una plantilla **Spark en el ejemplo de ejecución de clúster de HDInsight (Scala)**.

   c. Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:

      - **Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala

      -  **SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola 

      ![Creación de un proyecto de depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Seleccione **Siguiente**.     
 
3. Hola siguiente **nuevo proyecto** ventana, Hola siguientes:

   ![Seleccione Hola Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. Escriba un nombre y una ubicación de proyecto.

   b. Hola **proyecto SDK** lista desplegable, seleccione **Java 1.8** para **inspirará 2.x** de clúster o seleccione **Java 1.7** para **Spark 1. x** clúster.

   c. Hola **versión Spark** lista desplegable, el Asistente para la creación de hello Scala proyecto integra la versión correcta de Hola para Spark SDK y Scala SDK. Si la versión de clúster de spark hello es anterior a la 2.0, seleccione **inspirará 1.x**. De lo contrario, seleccione **Spark 2.x**. Este ejemplo utiliza **Spark 2.0.2 (Scala 2.11.8)**.

   d. Seleccione **Finalizar**.

4. Seleccione **src** > **principal** > **scala** tooopen el código en proyectos de Hola. Este ejemplo utiliza hello **SparkCore_wasbloTest** secuencia de comandos.

5. Hola tooaccess **editar configuraciones** menú, el icono de hello select en la esquina superior derecha de Hola. En este menú, puede crear o editar configuraciones de hello para la depuración remota.

   ![Editar configuraciones](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. Hola **las configuraciones de ejecución y depuración** cuadro de diálogo, seleccione hello además de inicio de sesión (**+**). A continuación, seleccione hello **enviar el trabajo de Spark** opción.

   ![Adición de nueva configuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. Escriba la información en los campos **Name** (Nombre), **Spark cluster** (Clúster de Spark) y **Main class name** (Nombre de clase principal). Después seleccione **Advanced configuration** (Configuración avanzada). 

   ![Ejecutar configuraciones de depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. Hola **Spark envío Advanced Configuration** cuadro de diálogo, seleccione **depuración remota habilitar Spark**. Escriba el nombre de usuario SSH de hello y, a continuación, escriba una contraseña o usar un archivo de clave privada. configuración de toosave hello, seleccione **Aceptar**.

   ![Habilitar la depuración remota de Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. configuración de Hello ahora se guarda con nombre hello especificado. detalles de configuración de hello tooview, nombre de la configuración de hello select. cambios de toomake, seleccione **editar configuraciones**. 

10. Después de completar la configuración de las configuraciones de hello, puede ejecutar el proyecto de hello en clúster remoto Hola o realizar una depuración remota.

## <a name="learn-how-tooperform-remote-debugging"></a>Obtenga información acerca de cómo tooperform la depuración remota
### <a name="scenario-1-perform-remote-run"></a>Escenario 1: Realizar la ejecución remota

En esta sección, le mostramos cómo toodebug controladores y elementos de ejecución.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Configurar puntos de interrupción y, a continuación, seleccione hello **depurar** icono.

   ![Seleccione el icono de depuración de Hola](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Cuando la ejecución del programa Hola alcanza el punto de interrupción de hello, verá un **controlador** ficha y dos **ejecutor** pestañas en hello **depurador** panel. Seleccione hello **reanudar programa** toocontinue de icono que se ejecuta el código de hello, que, a continuación, alcanza el punto de interrupción siguiente hello y se centra en hello correspondiente **ejecutor** ficha. Puede revisar los registros de ejecución de hello en hello correspondiente **consola** ficha.

   ![Pestaña Depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Escenario 2: Realizar la depuración remota y la corrección de errores
En esta sección, se muestra cómo toodynamically actualización Hola valor de la variable mediante el uso de Hola IntelliJ funcionalidades para una solución sencilla de depuración. En el siguiente ejemplo de código de hello, se produce una excepción porque ya existe el archivo de destino de hello.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>depuración remota de tooperform y corrección de errores
1. Configurar dos puntos de interrupción y, a continuación, seleccione hello **depurar** Hola de toostart icono proceso de depuración remota.

2. código de Hello se detiene en el primer punto de interrupción de Hola y parámetro hello y la información sobre las variable se muestran en hello **Variables** panel. 

3. Seleccione hello **reanudar programa** toocontinue de icono. código de Hello se detiene en el segundo punto de Hola. se detectó la excepción de Hello según lo previsto.

  ![Iniciar error](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Seleccione hello **reanudar programa** nuevo icono. Hola **HDInsight Spark envío** ventana muestra un error de "Error de la ejecución de trabajo".

  ![Envío de error](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. toodynamically actualización Hola valor de la variable mediante el uso de hello IntelliJ las capacidades de depuración, seleccione **depurar** nuevo. Hola **Variables** panel aparece de nuevo. 

6. Menú contextual destino de hello en hello **depurar** pestaña y, a continuación, seleccione **establecer valor**. A continuación, escriba un nuevo valor para la variable de saludo. A continuación, seleccione **ENTRAR** valor de hello toosave. 

  ![Establecer valor](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Seleccione hello **reanudar programa** programa Hola de icono toocontinue toorun. Esta vez no se detecta ninguna excepción. Puede ver que ese proyecto Hola se ejecuta correctamente sin ninguna excepción.

  ![Depurar sin excepciones](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Pasos siguientes
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demostración
* Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)
* Depuración remota (vídeo): [Use Azure Toolkit IntelliJ toodebug Spark para aplicaciones de forma remota en un clúster de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Escenarios
* [Spark con BI: realización del análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con aprendizaje automático: Use Spark en tooanalyze HDInsight generar temperatura utilizando los datos HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [La transmisión por secuencias Spark: Use Spark en HDInsight toobuild aplicaciones de transmisión por secuencias en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Usar el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de un clúster de HDInsight](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar el Kit de herramientas de Azure para las aplicaciones de IntelliJ toodebug Spark forma remota a través de VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Clúster de núcleos disponibles para Jupyter notebook Hola Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)
