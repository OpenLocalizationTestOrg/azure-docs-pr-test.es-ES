---
title: Kit de herramientas para Eclipse - Scala crear aplicaciones para HDInsight Spark aaaAzure | Documentos de Microsoft
description: "Usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Spark de Eclipse toodevelop escritas en Scala y enviarlos tooan clúster de HDInsight Spark, directamente desde ellos Hola Eclipse IDE."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Usar el Kit de herramientas de Azure Eclipse toocreate Spark para las aplicaciones de un clúster de HDInsight

Use herramientas de HDInsight en el Kit de herramientas de Azure para Eclipse toodevelop inspirará las aplicaciones escritas en Scala y envían en un clúster de Azure HDInsight Spark tooan, directamente desde Hola Eclipse IDE. Puede usar herramientas de HDInsight de hello complemento de varias maneras diferentes:

* toodevelop y enviar una solicitud de Scala Spark en un clúster de HDInsight Spark
* tooaccess los recursos de clúster de Azure HDInsight Spark
* toodevelop y ejecutar una aplicación Scala Spark localmente

> [!IMPORTANT]
> Esta herramienta puede ser toocreate usado y enviar solicitudes para un clúster de HDInsight Spark en Linux.
> 
> 

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit versión 8, que se usa para el tiempo de ejecución de hello Eclipse IDE. Puede descargarlo en hello [sitio Web de Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IDE de Eclipse. En este artículo se utiliza Eclipse Neon. Puede instalarlo desde hello [sitio Web de Eclipse](https://www.eclipse.org/downloads/).   
* SDK de Spark. Puede descargarlo en [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Instalar herramientas de HDInsight en el Kit de herramientas de Azure para Eclipse y Scala complemento
### <a name="install-hdinsight-tools"></a>Instalación de las herramientas de HDInsight
Las herramientas de HDInsight para Eclipse están disponibles como parte del kit de herramientas de Azure para Eclipse. Para obtener instrucciones de instalación, consulte [Instalación del Kit de herramientas de Azure para Eclipse](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Instale el complemento de Scala
Al abrir hello Intellij, hello HDInsight Tools automático detecta si instaló el complemento Scala o no. Haga clic en **Aceptar** toocontinue y seguir tooinstall de instrucciones de Hola por hello Marketplace de Eclipse.

 ![Complemento de Scala de instalación automática](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Inicie sesión en tooyour suscripción de Azure
1. Iniciar Hola Eclipse IDE y abra el Explorador de Azure. En hello **ventana** menú, haga clic en **Mostrar vista**y, a continuación, haga clic en **otros**. En el cuadro de diálogo de Hola que aparece, expanda **Azure**, haga clic en **explorador Azure**y, a continuación, haga clic en **Aceptar**.

    ![Cuadro de diálogo Show View (Mostrar vista)](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Menú contextual hello **Azure** nodo y, a continuación, haga clic en **iniciar sesión en**.
3. Hola **inicio de sesión en Azure** diálogo cuadro, elija el método de autenticación de hello, haga clic en **iniciar sesión en**y escriba sus credenciales de Azure.
   
    ![Cuadro de diálogo de inicio de sesión en Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. Después de que ha iniciado sesión, Hola **seleccione suscripciones** cuadro de diálogo enumera todos hello Azure suscripciones asociadas con las credenciales de Hola. Haga clic en **seleccione** cuadro de diálogo de tooclose Hola.

    ![Cuadro de diálogo de selección de suscripciones](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. En hello **explorador Azure** , expanda **HDInsight** hello toosee clústeres de HDInsight Spark bajo su suscripción.
   
    ![Clústeres de HDInsight Spark en Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. Expandir un nombre nodo toosee Hola recursos de clúster (por ejemplo, cuentas de almacenamiento) asociado con el clúster de Hola.
   
    ![Al expandir un recursos toosee de nombre de clúster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Configuración de un proyecto Spark en Scala de un clúster Spark en HDInsight

1. En el área de trabajo de Eclipse IDE hello, haga clic en **archivo**, haga clic en **New**y, a continuación, haga clic en **proyecto**. 
2. En el Asistente para nuevo proyecto de hello, expanda **HDInsight**, seleccione **Spark en HDInsight (Scala)**y, a continuación, haga clic en **siguiente**.

    ![Seleccionar Hola Spark en HDInsight (Scala) proyecto](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. automática de Asistente de creación de Hello Scala proyecto detecta si instaló el complemento Scala o no. Haga clic en **Aceptar** toocontinue descargar Hola Scala complemento y, a continuación, siga Hola instrucciones toorestart Eclipse.

    ![comprobación de scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. Hola **HDInsight Scala proyecto** cuadro de diálogo, proporcione Hola después de valores y, a continuación, haga clic en **siguiente**:
   * Escriba un nombre para el proyecto de Hola.
   * Hola **JRE** área, asegúrese de que **usar un entorno de ejecución JRE** se establece demasiado**JavaSE 1.7** o una versión posterior.
   * Asegúrese de que Spark SDK es conjunto toohello ubicación donde descargó Hola SDK. ubicación del vínculo de descarga toohello Hello se incluye una Hola [requisitos previos](#prerequisites) anteriormente en este artículo. También puede descargar Hola SDK de hello vínculo incluido en el cuadro de diálogo de Hola.

    ![Cuadro de diálogo nuevo proyecto de Scala para HDInsight](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  En el siguiente cuadro de diálogo hello, haga clic en hello **bibliotecas** pestaña y mantener los valores predeterminados de hello y, a continuación, haga clic en **finalizar**. 
   
    ![Pestaña de bibliotecas](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Creación de una aplicación de Scala para un clúster de HDInsight Spark

1. Hola Eclipse IDE, desde el Explorador de paquetes, expanda el proyecto de Hola que creó anteriormente, haga clic en **src**, seleccione demasiado**New**y, a continuación, haga clic en **otros**.
2. Hola **seleccionar un asistente** cuadro de diálogo, expanda **Scala asistentes**, haga clic en **objeto Scala**y, a continuación, haga clic en **siguiente**.
   
    ![Cuadro de diálogo de selección de asistente](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. Hola **crear un nuevo archivo** cuadro de diálogo, escriba un nombre para el objeto de hello y, a continuación, haga clic en **finalizar**.
   
    ![Cuadro de diálogo de creación de nuevo archivo](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Pegue Hola siguiente código en el editor de texto hello:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Ejecutar la aplicación hello en un clúster de HDInsight Spark:
   
   1. Desde el Explorador de paquetes, haga clic en el nombre del proyecto de hello y, a continuación, seleccione **tooHDInsight enviar Spark aplicación**.        
   2. Hola **Spark envío** cuadro de diálogo, proporcione Hola después de valores y, a continuación, haga clic en **enviar**:
      
      * Para **nombre del clúster**, seleccione Hola clúster de HDInsight Spark en el que desea que toorun la aplicación.
      * Seleccione un artefacto de proyectos de Eclipse hello, o uno desde una unidad de disco duro. valor predeterminado de Hello depende del elemento de hello que haga desde el Explorador de paquetes.
      * Hola **nombre de la clase principal** dropdownlist, envío asistente muestra todos los nombres de objeto desde el proyecto seleccionado. Seleccione o uno de entrada que desea toorun. Si selecciona un artefacto del disco duro, debe escribir el nombre de la clase principal. 
      * Porque no requieren argumentos de línea de comandos o no hacer referencia a archivos JAR o archivos de código de la aplicación hello en este ejemplo, puede dejar Hola restantes cuadros de texto vacíos.
        
       ![Cuadro de diálogo de envío de Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Hola **Spark envío** ficha debe comenzar a mostrar el progreso de Hola. Puede detener la aplicación hello haciendo clic en botón rojo Hola Hola **Spark envío** ventana. También puede ver registros de Hola para esta aplicación específica ejecute haciendo clic en el icono de globo de hello (indicado por el cuadro de color azul de hello en imagen de hello).
      
       ![Ventana de envío de Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Acceso y administración de clústeres HDInsight Spark mediante las herramientas de HDInsight del kit de herramientas de Azure para Eclipse
Puede realizar varias operaciones mediante herramientas de HDInsight, incluido el acceso a la salida del trabajo Hola.

### <a name="access-hello-job-view"></a>Vista de trabajos de Hola de acceso
1. En el Explorador de Azure, expanda **HDInsight**, expanda el nombre del clúster de Spark hello y, a continuación, haga clic en **trabajos**. 

    ![Nodo Vista de trabajos](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Haga clic en hello **trabajos** nodo. Herramientas de HDInsight de Hello detecta automáticamente si ha instalado Hola E (fx) clipse complemento o no. Haga clic en **Aceptar** toocontinue y seguir instrucciones de hello tooinstall Hola Marketplace de Eclipse y reinicie Eclipse.

    ![Instalación de E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Hola Abrir vista de trabajos de hello **trabajos** nodo. En el panel derecho de hello, Hola **Spark trabajo vista** ficha muestra todas las aplicaciones de Hola que se ejecutaron en clúster de Hola. Haga clic en hello aplicación hello para el que desea toosee más detalles.

    ![Detalles de aplicación](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Si mantiene el mouse en el gráfico de trabajo de hello, muestra información de trabajo de ejecución básica. Al hacer clic en el gráfico de trabajo de hello muestran gráfico de fases de Hola y la información que genera cada trabajo.

    ![Detalles de fase de trabajo](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Registros de usados frecuente, incluidos controlador Stderr y Stdout de controlador, la información del directorio, se muestran en hello **registro** ficha.

    ![Detalles del registro](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. También puede abrir historial Spark interfaz de usuario de Hola y Hola YARN interfaz de usuario (en el nivel de aplicación Hola) haciendo clic en hello hipervínculo respectivos en parte superior de Hola de ventana hello.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Contenedor de almacenamiento de Hola de acceso para el clúster de Hola
1. En el Explorador de Azure, expanda hello **HDInsight** toosee de nodo raíz una lista de clústeres de HDInsight Spark que están disponibles.
2. Expanda la cuenta de almacenamiento de hello clúster nombre toosee hello y contenedor de almacenamiento predeterminado de hello para el clúster de Hola.
   
    ![Cuenta de almacenamiento y contenedor de almacenamiento predeterminado](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Haga clic en el nombre del contenedor de almacenamiento de hello asociada Hola clúster. En el panel derecho de hello, haga doble clic en hello **HVACOut** carpeta. Abra uno de hello **parte -** archivos de salida de hello toosee de aplicación hello.

### <a name="access-hello-spark-history-server"></a>Servidor de acceso Hola Spark historial
1. En Azure Explorer, haga clic con el botón derecho en el nombre del clúster Spark y seleccione **Open Spark History UI** (Abrir IU de historial de Spark). Cuando se le pida, escriba las credenciales de administrador de hello para el clúster de Hola. Es necesario especificar estos al aprovisionar el clúster de Hola.
2. En el panel del servidor de hello Spark historial, se usa toolook de nombre de aplicación Hola para aplicación hello que simplemente terminado de ejecutarse. En el anterior código de hello, establecer nombre de la aplicación hello mediante `val conf = new SparkConf().setAppName("MyClusterApp")`. Por lo tanto, el nombre de aplicación Spark era **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Iniciar hello Ambari portal
1. En Azure Explorer, haga clic con el botón derecho en el nombre del clúster de Spark y seleccione **Open Cluster Management Portal (Ambari)** (Abrir portal de administración de clústeres [Ambari]). 
2. Cuando se le pida, escriba las credenciales de administrador de hello para el clúster de Hola. Es necesario especificar estos al aprovisionar el clúster de Hola.

### <a name="manage-azure-subscriptions"></a>Administración de suscripciones de Azure
De forma predeterminada, las herramientas de HDInsight de Azure Toolkit for Eclipse enumera los clústeres de Spark Hola de todas las suscripciones de Azure. Si es necesario, puede especificar las suscripciones de hello para el que desea que el clúster de Hola de tooaccess. 

1. En el Explorador de Azure, haga clic en hello **Azure** nodo raíz y, a continuación, haga clic en **administrar suscripciones**. 
2. En el cuadro de diálogo de hello, desactive casillas de verificación de hello para la suscripción de Hola que no desee tooaccess y, a continuación, haga clic en **cerrar**. También puede hacer clic en **cerrar sesión** si desea toosign fuera de su suscripción de Azure.

## <a name="run-a-spark-scala-application-locally"></a>Ejecución local de una aplicación Spark en Scala
Puede utilizar herramientas de HDInsight en el Kit de herramientas de Azure para Eclipse toorun Spark Scala aplicaciones localmente en la estación de trabajo. Normalmente, estas aplicaciones no necesitan tener acceso a recursos de toocluster como un contenedor de almacenamiento, y se puede ejecutar y se prueban localmente.

### <a name="prerequisite"></a>Requisito previo
Mientras se ejecuta la aplicación local de Spark Scala de hello en un equipo Windows, podría obtener una excepción, como se explica en [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Esta excepción se produce porque falta **WinUtils.exe** en Windows. 

tooresolve este error, debe [descargar ejecutable hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) como ubicación de tooa **C:\WinUtils\bin**. A continuación, debe agregar la variable de entorno de hello **HADOOP_HOME** y establezca el valor de Hola de variable de hello demasiado**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Ejecución de una aplicación Spark en Scala local
1. Inicie Eclipse y cree un proyecto. Hola **nuevo proyecto** cuadro de diálogo, asegúrese de hello siguientes opciones y, a continuación, haga clic en **siguiente**.
   
   * En el panel izquierdo de hello, seleccione **HDInsight**.
   * En el panel derecho de hello, seleccione **Spark en HDInsight Local ejecutar ejemplo (Scala)**.

    ![Cuadro de diálogo Nuevo proyecto](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. Detalles del proyecto tooprovide hello, siga los pasos 3 a 6 de Hola sección anterior [configurar un proyecto de Spark Scala para un clúster de HDInsight Spark](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. plantilla de Hello agrega un código de ejemplo (**LogQuery**) en hello **src** carpeta que puede ejecutar localmente en el equipo.
   
    ![Ubicación de LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Hola contextual **LogQuery** aplicación, elija demasiado**ejecución**y, a continuación, haga clic en **1 aplicación Scala**. Verá un resultado similar al siguiente en hello **consola** ficha situada en la parte inferior de hello:
   
   ![Resultado de la ejecución local de la aplicación Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>P+F
elegir un almacén de aplicación tooAzure Data Lake, toosubmit **Interactive** modo durante el proceso de Hola de inicio de sesión Azure. Si selecciona el modo **Automatizado**, puede aparecer un error.

![inicio de sesión interactivo](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

Ahora se ha resuelto. Puede elegir la aplicación de un clúster de Azure datos Lake toosubmit con cualquier método de inicio de sesión.

## <a name="feedback-and-known-issues"></a>Comentarios y problemas conocidos
Actualmente, la visualización de salidas de Spark directamente no se admite.

Si tiene sugerencias o comentarios, o si encuentra algún problema al usar esta herramienta, sentirse toosend libre nos un correo electrónico en hdivstool@microsoft.com.

## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Escenarios
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análisis del registro del sitio web con Spark en HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Creación y ejecución de aplicaciones
* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Herramientas y extensiones
* [Utilizar el Kit de herramientas de Azure para IntelliJ toocreate y enviar Spark Scala aplicaciones](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar el Kit de herramientas de Azure para las aplicaciones de IntelliJ toodebug Spark forma remota a través de VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar el Kit de herramientas de Azure para aplicaciones de Spark IntelliJ toodebug forma remota a través de SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)

