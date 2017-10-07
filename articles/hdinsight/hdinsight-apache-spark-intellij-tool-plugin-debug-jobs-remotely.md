---
title: "Kit de herramientas para IntelliJ - aplicaciones de depuración remota en HDInsight Spark aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de depuración de tooremotely IntelliJ ejecutan en clústeres de HDInsight Spark a través de vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Usar el Kit de herramientas de Azure IntelliJ toodebug para aplicaciones de forma remota en HDInsight Spark a través de VPN

Se recomienda manera Hola de depurar remotamente a través de spark applicaltion ssh. Para obtener instrucciones, vea [Depuración de aplicaciones de Spark de forma remota en un clúster de HDInsight con el kit de herramientas de Azure para IntelliJ mediante SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Este artículo proporciona instrucciones paso a paso acerca de cómo toouse Hola herramientas de HDInsight en el Kit de herramientas de Azure para IntelliJ toosubmit un trabajo de Spark en HDInsight Spark clúster y, a continuación, depurarlo de forma remota desde el equipo de escritorio. toodo por lo tanto, debe realizar Hola siguiendo los pasos de alto nivel:

1. Creación de una red virtual de Azure de sitio a sitio o de punto a sitio. pasos de Hello en este documento se supone que usa una red de sitio a sitio.
2. Crear un clúster de Spark en HDInsight de Azure que forma parte de hello sitio a sitio red Virtual de Azure.
3. Compruebe la conectividad de hello entre el nodo principal del clúster de Hola y el escritorio.
4. Creación de una aplicación Scala en IntelliJ IDEA y configuración para la depuración remota.
5. Ejecutar y depurar la aplicación hello.

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un clúster de Apache Spark en HDInsight. Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).
* Kit de desarrollo de Oracle Java. Puede instalarlo desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. En este artículo se usa la versión 2017.1. Puede instalarlo desde [aquí](https://www.jetbrains.com/idea/download/).
* Herramientas de HDInsight del kit de herramientas de Azure para IntelliJ Herramientas de HDInsight para IntelliJ están disponibles como parte del Kit de herramientas de Azure para IntelliJ Hola. Para obtener instrucciones sobre cómo tooinstall Hola Kit de herramientas de Azure, consulte [instalar hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Inicie sesión en la suscripción de Azure desde IntelliJ IDEA. Siga las instrucciones de hello [aquí](hdinsight-apache-spark-intellij-tool-plugin.md).
* Mientras se ejecuta la aplicación Scala Spark para la depuración remota en un equipo Windows, podría obtener una excepción, como se explica en [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) que se produce debido a falta de tooa WinUtils.exe en Windows. toowork solucionar este error, debe [descargar ejecutable hello desde aquí](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) como ubicación de tooa **C:\WinUtils\bin**. A continuación, debe agregar una variable de entorno **HADOOP_HOME** y establezca el valor de Hola de variable de hello demasiado**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Paso 1: Creación de una red virtual de Azure
Siga las instrucciones de Hola de hello debajo de vínculos toocreate una red Virtual de Azure y, a continuación, compruebe la conectividad de hello entre escritorio hello y red Virtual de Azure.

* [Creación de una red virtual con una conexión VPN de sitio a sitio mediante el Portal de Azure y Azure Resource Manager](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Creación de una red virtual con una conexión VPN de sitio a sitio mediante Azure Resource Manager y PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Configurar una red virtual de sitio de punto de conexión tooa con PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Paso 2: Creación de un clúster de Spark en HDInsight
También debe crear un clúster de Apache Spark en HDInsight de Azure que forma parte del programa Hola a red Virtual de Azure que ha creado. Use Hola información disponible en [basados en Linux crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Como parte de la configuración opcional, seleccione Hola red Virtual de Azure que creó en el paso anterior de Hola.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Paso 3: Comprobar la conectividad de hello entre el nodo principal del clúster de Hola y el escritorio
1. Obtener dirección IP de Hola de nodo principal de Hola. Abra Ambari UI para clúster Hola. En la hoja de clúster de hello, haga clic en **panel**.

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. En hello Ambari UI, desde la esquina superior derecha de hello, haga clic en **Hosts**.

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Debería ver una lista de nodos principales, nodos de trabajo y nodos de Zookeeper. Hola headnodes tienen hello **hn*** prefijo. Haga clic en el nodo principal primera Hola.

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Final de Hola de página de Hola que se abre desde hello **resumen** cuadro de dirección IP de hello copia del nodo principal de Hola y el nombre de host de Hola.

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Incluir dirección IP de Hola y el nombre de host de Hola de hello nodo principal toohello **hosts** archivo hello equipo desde donde desea toorun y depurar de forma remota los trabajos de Spark Hola. Esto le permitirá toocommunicate con el nodo principal de hello mediante la dirección IP de hello, así como el nombre de host de Hola.

   1. Abra el Bloc de notas con permisos elevados. En el menú archivo de hello, haga clic en **abiertos** y, a continuación, navegue toohello ubicación del archivo de hosts de Hola. En un equipo Windows, es `C:\Windows\System32\Drivers\etc\hosts`.
   2. Agregar Hola después toohello **hosts** archivo.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Desde equipo Hola había conectado toohello red Virtual de Azure que se usa por clúster de HDInsight de hello, compruebe que puede hacer ping en ambos headnodes Hola utilizando la dirección IP de hello, así como el nombre de host de Hola.
7. SSH en el nodo principal de clúster de hello mediante instrucciones de hello en [clúster de HDInsight de tooan conectar mediante SSH](hdinsight-hadoop-linux-use-ssh-unix.md). Desde el nodo principal del clúster de hello, haga ping a dirección IP de Hola de equipo de escritorio de Hola. Debe probar conectividad tooboth Hola IP direcciones asignadas toohello equipo, uno para la conexión de red de Hola y Hola otro para hello red Virtual de Azure que Hola equipo está conectado a.
8. Repita los pasos de Hola para hello y otro nodo principal.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Paso 4: Crear una aplicación de Spark Scala mediante herramientas de HDInsight de hello en el Kit de herramientas de Azure para IntelliJ y configurarlo para la depuración remota
1. Inicie IntelliJ IDEA y cree un nuevo proyecto. En el cuadro de diálogo de proyecto nuevo hello, asegúrese de Hola siguientes opciones y, a continuación, haga clic en **siguiente**.

    ![Crear aplicación Spark en Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * En el panel izquierdo de hello, seleccione **HDInsight**.
   * En el panel derecho de hello, seleccione **Spark en HDInsight (Scala)**.
   * Haga clic en **Siguiente**.
2. En la siguiente ventana de hello, proporcionar Hola siguiendo los detalles del proyecto y, a continuación, haga clic en **finalizar**.  
   - Proporcione un nombre de proyecto y la ubicación del proyecto.
   - En **Project SDK** (SDK de proyecto), use Java 1.8 para el clúster Spark 2.x o Java 1.7 para el clúster Spark 1.x.
   - En **Spark Version** (Versión de Spark), el Asistente para crear un proyecto de Scala integra la versión correcta del SDK de Spark y el SDK de Scala. Si la versión de clúster de spark hello es 2.0 inferior, elija inspirará 1.x. En caso contrario, debe seleccionar spark2.x. Este ejemplo utiliza Spark2.0.2 (Scala 2.11.8).
       ![Creación de una aplicación Spark en Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. proyecto de Spark Hola creará automáticamente un artefacto. artefacto de hello toosee, siga estos pasos.

   1. De hello **archivo** menú, haga clic en **estructura del proyecto**.
   2. Hola **estructura del proyecto** cuadro de diálogo, haga clic en **artefactos** artefacto de predeterminado de hello toosee que se crea.
   ![Crear un JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      También puede crear su propios artefacto bly al hacer clic en hello ** + ** icono, resaltado en la imagen de hello anterior.

4. Agregar proyecto de bibliotecas tooyour. tooadd una biblioteca, haga clic en nombre de proyecto de hello en el árbol del proyecto de hello y, a continuación, haga clic en **configuración para abrir el módulo**. Hola **estructura del proyecto** cuadro de diálogo, en el panel izquierdo de hello, haga clic en **bibliotecas**, haga clic en el símbolo de hello (+) y, a continuación, haga clic en **de Maven**.

    ![Agregar biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    Hola **Download Library desde el repositorio de Maven** diálogo cuadro, buscar y agregar Hola siguiendo las bibliotecas.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Copia `yarn-site.xml` y `core-site.xml` de hello nodo principal del clúster y Agregar proyecto toohello. Usar hello siguientes archivos de comandos toocopy Hola. Puede usar [Cygwin](https://cygwin.com/install.html) siguiente de hello toorun `scp` comandos toocopy archivos de Hola de hello headnodes de clúster.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Porque ya se han agregado Hola clúster nodo principal IP direcciones y nombres de host fo Hola archivo hosts en el escritorio de hello, podemos usar hello **scp** comandos Hola siguiente manera.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Agregar un proyecto tooyour de estos archivos, cópielos en hello **/src** carpeta en el árbol del proyecto, por ejemplo `<your project directory>\src`.
6. Hola de actualización `core-site.xml` hello toomake después de cambios.

   1. `core-site.xml`incluye las cuentas de almacenamiento de toohello clave Hola cifrado asociada con el clúster de Hola. Hola `core-site.xml` que ha agregado el proyecto toohello, replace Hola clave cifrada con la clave de almacenamiento real de hello asociado a la cuenta de almacenamiento predeterminada de Hola. Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Quitar Hola siguientes entradas de hello `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Guarde el archivo hello.
7. Agregar clase de hello principal para la aplicación. De hello **el Explorador de proyectos**, haga clic en **src**, seleccione demasiado**New**y, a continuación, haga clic en **Scala clase**.

    ![Agregar código fuente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. Hola **crear nueva clase Scala** diálogo cuadro, proporcione un nombre para **tipo** seleccione **objeto**y, a continuación, haga clic en **Aceptar**.

    ![Agregar código fuente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. Hola `MyClusterAppMain.scala` de archivo, pegue el siguiente código de hello. Este código crea el contexto de Spark Hola e inicia un `executeJob` método de hello `SparkSample` objeto.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Repita los pasos 8 y 9 anteriormente tooadd llama a un nuevo objeto Scala `SparkSample`. clase toothis agregar Hola siguiente código. Este código lee los datos de Hola de hello HVAC.csv (disponible en todos los clústeres de HDInsight Spark), se recuperan las filas de Hola que sólo tienen un dígito en la columna séptimo Hola Hola CSV y escribe la salida de hello demasiado**/HVACOut** en el valor predeterminado de Hola contenedor de almacenamiento de clúster de Hola.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Repita los pasos 8 y 9 anteriormente tooadd una nueva clase denominada `RemoteClusterDebugging`. Esta clase implementa el marco de pruebas de Spark Hola que se usa para depurar aplicaciones. Agregar Hola después código toohello `RemoteClusterDebugging` clase.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Par de cosas importantes toonote aquí:

   * Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, asegúrese de que está disponible en el almacenamiento de clúster de hello en la ruta de acceso especificada de Hola Hola ensamblado Spark JAR.
   * Para `setJars`, especificar ubicación de Hola donde se creará el archivo jar de artefacto de Hola. Normalmente es `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. Hola `RemoteClusterDebugging` de clases, haga clic en hello `test` palabra clave y seleccione **crear configuración de RemoteClusterDebugging**.

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. En el cuadro de diálogo de hello, proporcione un nombre para la configuración de Hola y seleccione hello **probar tipo** como **nombre de la prueba**. Deje los demás valores predeterminados y haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Ahora debería ver un **ejecutar remoto** configuración de lista desplegable en la barra de menús de Hola.

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Paso 5: Ejecutar la aplicación hello en modo de depuración
1. En el proyecto IntelliJ IDEA, abra `SparkSample.scala` y crear un rdd1 de punto de interrupción siguiente too'val'. En el menú emergente de Hola para crear un punto de interrupción, seleccione **línea en la función executeJob**.

    ![Agregar un punto de interrupción](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Haga clic en hello **depurar ejecutar** botón siguiente toohello **ejecutar remoto** toostart de lista desplegable de configuración ejecutando la aplicación hello.

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Cuando la ejecución del programa Hola alcanza el punto de interrupción de hello, debería ver un **depurador** ficha en el panel inferior de Hola.

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Haga clic en hello (**+**) tooadd icono una inspección como se muestra en la imagen de hello siguiente.

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Aquí, porque se interrumpió la aplicación hello antes de la variable de hello `rdd1` se creó con esta inspección podemos ver lo que se Hola primeras 5 filas en la variable de hello `rdd`. Presione **ENTRAR**.

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    Lo que ve en la imagen de hello anterior es que en tiempo de ejecución, puede consultar terabytes de datos y de depuración cómo progresa de su aplicación. Por ejemplo, en la salida de hello se muestra en la imagen de hello anterior, puede ver que Hola primera fila de salida de hello es un encabezado. En función de esto, puede modificar la fila de encabezado de aplicación código tooskip Hola si es necesario.
5. Ahora puede hacer clic hello **reanudar programa** tooproceed icono con la ejecución de la aplicación.

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Si finaliza correctamente la aplicación hello, debería ver un resultado similar Hola siguiente.

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Otras referencias
* [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demostración
* Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)
* Depuración remota (vídeo): [Use Azure Toolkit IntelliJ toodebug Spark para aplicaciones de forma remota en clúster de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

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
* [Usar herramientas de HDInsight en el Kit de herramientas de Azure para IntelliJ toocreate y enviar Spark Scala aplicaciones](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar el Kit de herramientas de Azure para aplicaciones de Spark IntelliJ toodebug forma remota a través de SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Uso de paquetes externos con cuadernos de Jupyter Notebook](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Administración de recursos
* [Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)](hdinsight-apache-spark-job-debugging.md)
