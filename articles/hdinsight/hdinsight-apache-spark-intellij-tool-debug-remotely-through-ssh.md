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
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="14b20-104">Depuración de aplicaciones Spark en un clúster de HDInsight con el Kit de herramientas de Azure para IntelliJ mediante SSH</span><span class="sxs-lookup"><span data-stu-id="14b20-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="14b20-105">Este artículo proporciona instrucciones paso a paso acerca de cómo toouse herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toodebug para aplicaciones de forma remota en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b20-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="14b20-106">toodebug el proyecto, también puede ver hello [aplicaciones depurar HDInsight Spark con el Kit de herramientas de Azure para IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) vídeo.</span><span class="sxs-lookup"><span data-stu-id="14b20-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="14b20-107">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="14b20-107">**Prerequisites**</span></span>

* <span data-ttu-id="14b20-108">**Herramientas de HDInsight del kit de herramientas de Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="14b20-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="14b20-109">Esta herramienta es parte del Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="14b20-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="14b20-110">Para más información, vea [Instalación del kit de herramientas de Azure para IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="14b20-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="14b20-111">**Kit de herramientas de Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="14b20-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="14b20-112">Use esta aplicación de Spark toocreate Kit de herramientas para un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b20-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="14b20-113">Para obtener más información, siga las instrucciones de hello en [Use Azure Toolkit IntelliJ toocreate Spark para las aplicaciones de un clúster de HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="14b20-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="14b20-114">**Servicio SSH de HDInsight con administración de nombre de usuario y contraseña**.</span><span class="sxs-lookup"><span data-stu-id="14b20-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="14b20-115">Para obtener más información, consulte [conectar tooHDInsight (Hadoop) a través de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y [utilizar SSH túneles tooaccess Ambari web UI, JobHistory, NameNode, Oozie y otras interfaces de usuario web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="14b20-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="14b20-116">Creación de una aplicación Scala de Spark y configuración para la depuración remota</span><span class="sxs-lookup"><span data-stu-id="14b20-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="14b20-117">Inicie IntelliJ IDEA y, después, cree un proyecto.</span><span class="sxs-lookup"><span data-stu-id="14b20-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="14b20-118">Hola **nuevo proyecto** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="14b20-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="14b20-119">a.</span><span class="sxs-lookup"><span data-stu-id="14b20-119">a.</span></span> <span data-ttu-id="14b20-120">Seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="14b20-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="14b20-121">b.</span><span class="sxs-lookup"><span data-stu-id="14b20-121">b.</span></span> <span data-ttu-id="14b20-122">Seleccione una plantilla de Java o Scala según sus preferencias.</span><span class="sxs-lookup"><span data-stu-id="14b20-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="14b20-123">Seleccione entre Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="14b20-123">Select between hello following options:</span></span>

      - <span data-ttu-id="14b20-124">**Spark en HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="14b20-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="14b20-125">**Spark en HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="14b20-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="14b20-126">**Spark en el ejemplo de ejecución de clúster de HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="14b20-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="14b20-127">En este ejemplo se usa una plantilla **Spark en el ejemplo de ejecución de clúster de HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="14b20-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="14b20-128">c.</span><span class="sxs-lookup"><span data-stu-id="14b20-128">c.</span></span> <span data-ttu-id="14b20-129">Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:</span><span class="sxs-lookup"><span data-stu-id="14b20-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="14b20-130">**Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="14b20-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="14b20-131">**SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola</span><span class="sxs-lookup"><span data-stu-id="14b20-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Creación de un proyecto de depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="14b20-133">d.</span><span class="sxs-lookup"><span data-stu-id="14b20-133">d.</span></span> <span data-ttu-id="14b20-134">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="14b20-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="14b20-135">Hola siguiente **nuevo proyecto** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="14b20-135">In hello next **New Project** window, do hello following:</span></span>

   ![Seleccione Hola Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="14b20-137">a.</span><span class="sxs-lookup"><span data-stu-id="14b20-137">a.</span></span> <span data-ttu-id="14b20-138">Escriba un nombre y una ubicación de proyecto.</span><span class="sxs-lookup"><span data-stu-id="14b20-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="14b20-139">b.</span><span class="sxs-lookup"><span data-stu-id="14b20-139">b.</span></span> <span data-ttu-id="14b20-140">Hola **proyecto SDK** lista desplegable, seleccione **Java 1.8** para **inspirará 2.x** de clúster o seleccione **Java 1.7** para **Spark 1. x** clúster.</span><span class="sxs-lookup"><span data-stu-id="14b20-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="14b20-141">c.</span><span class="sxs-lookup"><span data-stu-id="14b20-141">c.</span></span> <span data-ttu-id="14b20-142">Hola **versión Spark** lista desplegable, el Asistente para la creación de hello Scala proyecto integra la versión correcta de Hola para Spark SDK y Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="14b20-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="14b20-143">Si la versión de clúster de spark hello es anterior a la 2.0, seleccione **inspirará 1.x**.</span><span class="sxs-lookup"><span data-stu-id="14b20-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="14b20-144">De lo contrario, seleccione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="14b20-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="14b20-145">Este ejemplo utiliza **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="14b20-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="14b20-146">d.</span><span class="sxs-lookup"><span data-stu-id="14b20-146">d.</span></span> <span data-ttu-id="14b20-147">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="14b20-147">Select **Finish**.</span></span>

4. <span data-ttu-id="14b20-148">Seleccione **src** > **principal** > **scala** tooopen el código en proyectos de Hola.</span><span class="sxs-lookup"><span data-stu-id="14b20-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="14b20-149">Este ejemplo utiliza hello **SparkCore_wasbloTest** secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="14b20-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="14b20-150">Hola tooaccess **editar configuraciones** menú, el icono de hello select en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="14b20-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="14b20-151">En este menú, puede crear o editar configuraciones de hello para la depuración remota.</span><span class="sxs-lookup"><span data-stu-id="14b20-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Editar configuraciones](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="14b20-153">Hola **las configuraciones de ejecución y depuración** cuadro de diálogo, seleccione hello además de inicio de sesión (**+**).</span><span class="sxs-lookup"><span data-stu-id="14b20-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="14b20-154">A continuación, seleccione hello **enviar el trabajo de Spark** opción.</span><span class="sxs-lookup"><span data-stu-id="14b20-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Adición de nueva configuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="14b20-156">Escriba la información en los campos **Name** (Nombre), **Spark cluster** (Clúster de Spark) y **Main class name** (Nombre de clase principal).</span><span class="sxs-lookup"><span data-stu-id="14b20-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="14b20-157">Después seleccione **Advanced configuration** (Configuración avanzada).</span><span class="sxs-lookup"><span data-stu-id="14b20-157">Then select **Advanced configuration**.</span></span> 

   ![Ejecutar configuraciones de depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="14b20-159">Hola **Spark envío Advanced Configuration** cuadro de diálogo, seleccione **depuración remota habilitar Spark**.</span><span class="sxs-lookup"><span data-stu-id="14b20-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="14b20-160">Escriba el nombre de usuario SSH de hello y, a continuación, escriba una contraseña o usar un archivo de clave privada.</span><span class="sxs-lookup"><span data-stu-id="14b20-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="14b20-161">configuración de toosave hello, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="14b20-161">toosave hello configuration, select **OK**.</span></span>

   ![Habilitar la depuración remota de Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="14b20-163">configuración de Hello ahora se guarda con nombre hello especificado.</span><span class="sxs-lookup"><span data-stu-id="14b20-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="14b20-164">detalles de configuración de hello tooview, nombre de la configuración de hello select.</span><span class="sxs-lookup"><span data-stu-id="14b20-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="14b20-165">cambios de toomake, seleccione **editar configuraciones**.</span><span class="sxs-lookup"><span data-stu-id="14b20-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="14b20-166">Después de completar la configuración de las configuraciones de hello, puede ejecutar el proyecto de hello en clúster remoto Hola o realizar una depuración remota.</span><span class="sxs-lookup"><span data-stu-id="14b20-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="14b20-167">Obtenga información acerca de cómo tooperform la depuración remota</span><span class="sxs-lookup"><span data-stu-id="14b20-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="14b20-168">Escenario 1: Realizar la ejecución remota</span><span class="sxs-lookup"><span data-stu-id="14b20-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="14b20-169">En esta sección, le mostramos cómo toodebug controladores y elementos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="14b20-169">In this section, we show you how toodebug drivers and executors.</span></span>

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


1. <span data-ttu-id="14b20-170">Configurar puntos de interrupción y, a continuación, seleccione hello **depurar** icono.</span><span class="sxs-lookup"><span data-stu-id="14b20-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Seleccione el icono de depuración de Hola](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="14b20-172">Cuando la ejecución del programa Hola alcanza el punto de interrupción de hello, verá un **controlador** ficha y dos **ejecutor** pestañas en hello **depurador** panel.</span><span class="sxs-lookup"><span data-stu-id="14b20-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="14b20-173">Seleccione hello **reanudar programa** toocontinue de icono que se ejecuta el código de hello, que, a continuación, alcanza el punto de interrupción siguiente hello y se centra en hello correspondiente **ejecutor** ficha. Puede revisar los registros de ejecución de hello en hello correspondiente **consola** ficha.</span><span class="sxs-lookup"><span data-stu-id="14b20-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Pestaña Depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="14b20-175">Escenario 2: Realizar la depuración remota y la corrección de errores</span><span class="sxs-lookup"><span data-stu-id="14b20-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="14b20-176">En esta sección, se muestra cómo toodynamically actualización Hola valor de la variable mediante el uso de Hola IntelliJ funcionalidades para una solución sencilla de depuración.</span><span class="sxs-lookup"><span data-stu-id="14b20-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="14b20-177">En el siguiente ejemplo de código de hello, se produce una excepción porque ya existe el archivo de destino de hello.</span><span class="sxs-lookup"><span data-stu-id="14b20-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
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


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="14b20-178">depuración remota de tooperform y corrección de errores</span><span class="sxs-lookup"><span data-stu-id="14b20-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="14b20-179">Configurar dos puntos de interrupción y, a continuación, seleccione hello **depurar** Hola de toostart icono proceso de depuración remota.</span><span class="sxs-lookup"><span data-stu-id="14b20-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="14b20-180">código de Hello se detiene en el primer punto de interrupción de Hola y parámetro hello y la información sobre las variable se muestran en hello **Variables** panel.</span><span class="sxs-lookup"><span data-stu-id="14b20-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="14b20-181">Seleccione hello **reanudar programa** toocontinue de icono.</span><span class="sxs-lookup"><span data-stu-id="14b20-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="14b20-182">código de Hello se detiene en el segundo punto de Hola.</span><span class="sxs-lookup"><span data-stu-id="14b20-182">hello code stops at hello second point.</span></span> <span data-ttu-id="14b20-183">se detectó la excepción de Hello según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="14b20-183">hello exception is caught as expected.</span></span>

  ![Iniciar error](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="14b20-185">Seleccione hello **reanudar programa** nuevo icono.</span><span class="sxs-lookup"><span data-stu-id="14b20-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="14b20-186">Hola **HDInsight Spark envío** ventana muestra un error de "Error de la ejecución de trabajo".</span><span class="sxs-lookup"><span data-stu-id="14b20-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Envío de error](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="14b20-188">toodynamically actualización Hola valor de la variable mediante el uso de hello IntelliJ las capacidades de depuración, seleccione **depurar** nuevo.</span><span class="sxs-lookup"><span data-stu-id="14b20-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="14b20-189">Hola **Variables** panel aparece de nuevo.</span><span class="sxs-lookup"><span data-stu-id="14b20-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="14b20-190">Menú contextual destino de hello en hello **depurar** pestaña y, a continuación, seleccione **establecer valor**.</span><span class="sxs-lookup"><span data-stu-id="14b20-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="14b20-191">A continuación, escriba un nuevo valor para la variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="14b20-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="14b20-192">A continuación, seleccione **ENTRAR** valor de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="14b20-192">Then select **Enter** toosave hello value.</span></span> 

  ![Establecer valor](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="14b20-194">Seleccione hello **reanudar programa** programa Hola de icono toocontinue toorun.</span><span class="sxs-lookup"><span data-stu-id="14b20-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="14b20-195">Esta vez no se detecta ninguna excepción.</span><span class="sxs-lookup"><span data-stu-id="14b20-195">This time, no exception is caught.</span></span> <span data-ttu-id="14b20-196">Puede ver que ese proyecto Hola se ejecuta correctamente sin ninguna excepción.</span><span class="sxs-lookup"><span data-stu-id="14b20-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Depurar sin excepciones](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="14b20-198"><a name="seealso"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14b20-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="14b20-199">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="14b20-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="14b20-200">Demostración</span><span class="sxs-lookup"><span data-stu-id="14b20-200">Demo</span></span>
* <span data-ttu-id="14b20-201">Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="14b20-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="14b20-202">Depuración remota (vídeo): [Use Azure Toolkit IntelliJ toodebug Spark para aplicaciones de forma remota en un clúster de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="14b20-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="14b20-203">Escenarios</span><span class="sxs-lookup"><span data-stu-id="14b20-203">Scenarios</span></span>
* [<span data-ttu-id="14b20-204">Spark con BI: realización del análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="14b20-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="14b20-205">Spark con aprendizaje automático: Use Spark en tooanalyze HDInsight generar temperatura utilizando los datos HVAC</span><span class="sxs-lookup"><span data-stu-id="14b20-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="14b20-206">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="14b20-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="14b20-207">La transmisión por secuencias Spark: Use Spark en HDInsight toobuild aplicaciones de transmisión por secuencias en tiempo real</span><span class="sxs-lookup"><span data-stu-id="14b20-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="14b20-208">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="14b20-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="14b20-209">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="14b20-209">Create and run applications</span></span>
* [<span data-ttu-id="14b20-210">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="14b20-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="14b20-211">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="14b20-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="14b20-212">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="14b20-212">Tools and extensions</span></span>
* [<span data-ttu-id="14b20-213">Usar el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="14b20-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="14b20-214">Usar el Kit de herramientas de Azure para las aplicaciones de IntelliJ toodebug Spark forma remota a través de VPN</span><span class="sxs-lookup"><span data-stu-id="14b20-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="14b20-215">Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="14b20-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="14b20-216">Usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark</span><span class="sxs-lookup"><span data-stu-id="14b20-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="14b20-217">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="14b20-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="14b20-218">Clúster de núcleos disponibles para Jupyter notebook Hola Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="14b20-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="14b20-219">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="14b20-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="14b20-220">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="14b20-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="14b20-221">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="14b20-221">Manage resources</span></span>
* [<span data-ttu-id="14b20-222">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="14b20-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="14b20-223">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="14b20-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
