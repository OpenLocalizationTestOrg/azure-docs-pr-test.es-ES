---
title: "Kit de herramientas de Azure para IntelliJ: depuración de aplicaciones Spark de forma remota mediante SSH | Microsoft Docs"
description: "Instrucciones paso a paso para el uso de las herramientas de HDInsight del Kit de herramientas de Azure para IntelliJ para depurar aplicaciones de forma remota en clústeres de HDInsight mediante SSH"
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
ms.openlocfilehash: 19053e31d6eb097bc91a04ef9c6af5772aaa16da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="8fc16-104">Depuración de aplicaciones Spark en un clúster de HDInsight con el Kit de herramientas de Azure para IntelliJ mediante SSH</span><span class="sxs-lookup"><span data-stu-id="8fc16-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="8fc16-105">En este artículo se ofrecen instrucciones paso a paso para el empleo de las herramientas de HDInsight del Kit de herramientas de Azure para IntelliJ para depurar aplicaciones de forma remota en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fc16-105">This article provides step-by-step guidance on how to use HDInsight Tools in Azure Toolkit for IntelliJ to debug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="8fc16-106">Para depurar el proyecto, también puede ver el vídeo [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ (Depurar aplicaciones HDInsight Spark con el Kit de herramientas de Azure para IntelliJ)](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="8fc16-106">To debug your project, you can also view the [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="8fc16-107">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="8fc16-107">**Prerequisites**</span></span>

* <span data-ttu-id="8fc16-108">**Herramientas de HDInsight del kit de herramientas de Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="8fc16-109">Esta herramienta es parte del Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8fc16-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="8fc16-110">Para más información, vea [Instalación del kit de herramientas de Azure para IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="8fc16-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="8fc16-111">**Kit de herramientas de Azure para IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="8fc16-112">Use este kit de herramientas para crear aplicaciones Spark para un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fc16-112">Use this toolkit to create Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="8fc16-113">Para más información, siga las instrucciones de [Uso del kit de herramientas de Azure para IntelliJ con el fin de crear aplicaciones Spark para un clúster de HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="8fc16-113">For more information, follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="8fc16-114">**Servicio SSH de HDInsight con administración de nombre de usuario y contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="8fc16-115">Para más información vea [Conexión a través de SSH con HDInsight (Hadoop)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) y [Uso de la tunelización SSH para tener acceso a la interfaz de usuario Ambari Web, JobHistory, NameNode, Oozie y otras interfaces de usuario web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="8fc16-115">For more information, see [Connect to HDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="8fc16-116">Creación de una aplicación Scala de Spark y configuración para la depuración remota</span><span class="sxs-lookup"><span data-stu-id="8fc16-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="8fc16-117">Inicie IntelliJ IDEA y, después, cree un proyecto.</span><span class="sxs-lookup"><span data-stu-id="8fc16-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="8fc16-118">En el cuadro de diálogo **Nuevo proyecto** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8fc16-118">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="8fc16-119">a.</span><span class="sxs-lookup"><span data-stu-id="8fc16-119">a.</span></span> <span data-ttu-id="8fc16-120">Seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="8fc16-121">b.</span><span class="sxs-lookup"><span data-stu-id="8fc16-121">b.</span></span> <span data-ttu-id="8fc16-122">Seleccione una plantilla de Java o Scala según sus preferencias.</span><span class="sxs-lookup"><span data-stu-id="8fc16-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="8fc16-123">Seleccione entre las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="8fc16-123">Select between the following options:</span></span>

      - <span data-ttu-id="8fc16-124">**Spark en HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="8fc16-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="8fc16-125">**Spark en HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="8fc16-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="8fc16-126">**Spark en el ejemplo de ejecución de clúster de HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="8fc16-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="8fc16-127">En este ejemplo se usa una plantilla **Spark en el ejemplo de ejecución de clúster de HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="8fc16-128">c.</span><span class="sxs-lookup"><span data-stu-id="8fc16-128">c.</span></span> <span data-ttu-id="8fc16-129">En la lista de **herramientas de compilación**, seleccione cualquiera de las siguientes, según sus necesidades:</span><span class="sxs-lookup"><span data-stu-id="8fc16-129">In the **Build tool** list, select either of the following, according to your need:</span></span>

      - <span data-ttu-id="8fc16-130">**Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="8fc16-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="8fc16-131">**SBT**, para administrar las dependencias y compilar el proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="8fc16-131">**SBT**, for managing the dependencies and building for the Scala project</span></span> 

      ![Creación de un proyecto de depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="8fc16-133">d.</span><span class="sxs-lookup"><span data-stu-id="8fc16-133">d.</span></span> <span data-ttu-id="8fc16-134">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="8fc16-135">En la siguiente ventana **Nuevo proyecto**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8fc16-135">In the next **New Project** window, do the following:</span></span>

   ![Selección del SDK de Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="8fc16-137">a.</span><span class="sxs-lookup"><span data-stu-id="8fc16-137">a.</span></span> <span data-ttu-id="8fc16-138">Escriba un nombre y una ubicación de proyecto.</span><span class="sxs-lookup"><span data-stu-id="8fc16-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="8fc16-139">b.</span><span class="sxs-lookup"><span data-stu-id="8fc16-139">b.</span></span> <span data-ttu-id="8fc16-140">En la lista desplegable **SDK de proyecto**, seleccione **Java 1.8** para el clúster de **Spark 2.x** o **Java 1.7** para el clúster de **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-140">In the **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="8fc16-141">c.</span><span class="sxs-lookup"><span data-stu-id="8fc16-141">c.</span></span> <span data-ttu-id="8fc16-142">En la lista desplegable **Versión de Spark**, el asistente para la creación de proyectos de Scala integra la versión correcta del SDK de Spark y el SDK de Scala.</span><span class="sxs-lookup"><span data-stu-id="8fc16-142">In the **Spark Version** drop-down list, the Scala project creation wizard integrates the correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="8fc16-143">Si la versión del clúster de Spark es anterior a la 2.0, seleccione **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-143">If the spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="8fc16-144">De lo contrario, seleccione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="8fc16-145">Este ejemplo utiliza **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="8fc16-146">d.</span><span class="sxs-lookup"><span data-stu-id="8fc16-146">d.</span></span> <span data-ttu-id="8fc16-147">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-147">Select **Finish**.</span></span>

4. <span data-ttu-id="8fc16-148">Seleccione **src** > **main** > **scala** para abrir el código en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8fc16-148">Select **src** > **main** > **scala** to open your code in the project.</span></span> <span data-ttu-id="8fc16-149">En este artículo se usa el script **SparkCore_wasbloTest**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-149">This example uses the **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="8fc16-150">Para acceder al menú **Editar configuraciones**, seleccione el icono de la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="8fc16-150">To access the **Edit Configurations** menu, select the icon in the upper-right corner.</span></span> <span data-ttu-id="8fc16-151">Desde este menú, puede crear o modificar las configuraciones para la depuración remota.</span><span class="sxs-lookup"><span data-stu-id="8fc16-151">From this menu, you can create or edit the configurations for remote debugging.</span></span>

   ![Editar configuraciones](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="8fc16-153">En el cuadro de diálogo **Run/Debug Configurations** (Ejecutar/depurar configuraciones), seleccione el signo más (**+**).</span><span class="sxs-lookup"><span data-stu-id="8fc16-153">In the **Run/Debug Configurations** dialog box, select the plus sign (**+**).</span></span> <span data-ttu-id="8fc16-154">Después, seleccione la opción **Submit Spark Job** (Enviar trabajo de Spark).</span><span class="sxs-lookup"><span data-stu-id="8fc16-154">Then select the **Submit Spark Job** option.</span></span>

   ![Adición de nueva configuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="8fc16-156">Escriba la información en los campos **Name** (Nombre), **Spark cluster** (Clúster de Spark) y **Main class name** (Nombre de clase principal).</span><span class="sxs-lookup"><span data-stu-id="8fc16-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="8fc16-157">Después seleccione **Advanced configuration** (Configuración avanzada).</span><span class="sxs-lookup"><span data-stu-id="8fc16-157">Then select **Advanced configuration**.</span></span> 

   ![Ejecutar configuraciones de depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="8fc16-159">En el cuadro de diálogo **Spark Submission Advanced Configuration** (Configuración avanzada de envío de Spark), seleccione **Enable Spark remote debug** (Habilitar depuración remota de Spark).</span><span class="sxs-lookup"><span data-stu-id="8fc16-159">In the **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="8fc16-160">Escriba el nombre de usuario SSH y luego especifique una contraseña o use un archivo de clave privada.</span><span class="sxs-lookup"><span data-stu-id="8fc16-160">Enter the SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="8fc16-161">Para guardar la configuración, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-161">To save the configuration, select **OK**.</span></span>

   ![Habilitar la depuración remota de Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="8fc16-163">La configuración se guarda ahora con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="8fc16-163">The configuration is now saved with the name you provided.</span></span> <span data-ttu-id="8fc16-164">Para ver los detalles de configuración, seleccione el nombre de configuración.</span><span class="sxs-lookup"><span data-stu-id="8fc16-164">To view the configuration details, select the configuration name.</span></span> <span data-ttu-id="8fc16-165">Para realizar cambios, seleccione **Edit Configurations** (Editar configuraciones).</span><span class="sxs-lookup"><span data-stu-id="8fc16-165">To make changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="8fc16-166">Después de completar la configuración, puede ejecutar el proyecto en el clúster remoto o realizar la depuración remota.</span><span class="sxs-lookup"><span data-stu-id="8fc16-166">After you complete the configurations settings, you can run the project against the remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-to-perform-remote-debugging"></a><span data-ttu-id="8fc16-167">Más información sobre la depuración remota</span><span class="sxs-lookup"><span data-stu-id="8fc16-167">Learn how to perform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="8fc16-168">Escenario 1: Realizar la ejecución remota</span><span class="sxs-lookup"><span data-stu-id="8fc16-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="8fc16-169">En esta sección, se muestra cómo depurar controladores y ejecutores.</span><span class="sxs-lookup"><span data-stu-id="8fc16-169">In this section, we show you how to debug drivers and executors.</span></span>

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
        /** Tracks the total query count and number of aggregate bytes for a particular group. */
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


1. <span data-ttu-id="8fc16-170">Configure puntos de interrupción y luego seleccione el icono **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-170">Set up breaking points, and then select the **Debug** icon.</span></span>

   ![Selección del icono de depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="8fc16-172">Cuando la ejecución del programa alcanza el punto de interrupción, aparecen una pestaña **Controlador** y dos pestañas **Ejecutor** en el panel **Depurador**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-172">When the program execution reaches the breaking point, you see a **Driver** tab and two **Executor** tabs in the **Debugger** pane.</span></span> <span data-ttu-id="8fc16-173">Seleccione el icono **Resume Program** (Continuar programa) para seguir ejecutando el código, que luego alcanza el siguiente punto de interrupción y se centra en la pestaña **Ejecutor** correspondiente. Puede revisar los registros de ejecución en la correspondiente pestaña **Consola**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-173">Select the **Resume Program** icon to continue running the code, which then reaches the next breakpoint and focuses on the corresponding **Executor** tab. You can review the execution logs on the corresponding **Console** tab.</span></span>

   ![Pestaña Depuración](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="8fc16-175">Escenario 2: Realizar la depuración remota y la corrección de errores</span><span class="sxs-lookup"><span data-stu-id="8fc16-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="8fc16-176">En esta sección, se muestra cómo actualizar dinámicamente el valor de la variable mediante el uso de la funcionalidad de depuración de IntelliJ para una revisión sencilla.</span><span class="sxs-lookup"><span data-stu-id="8fc16-176">In this section, we show you how to dynamically update the variable value by using the IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="8fc16-177">En el ejemplo de código siguiente, se produce una excepción porque el archivo de destino ya existe.</span><span class="sxs-lookup"><span data-stu-id="8fc16-177">In the following code example, an exception is thrown because the target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find the rows that have only one digit in the sixth column.
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


#### <a name="to-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="8fc16-178">Para realizar la depuración remota y la corrección de errores</span><span class="sxs-lookup"><span data-stu-id="8fc16-178">To perform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="8fc16-179">Configure dos puntos de interrupción y luego seleccione el icono **Depurar** para iniciar el proceso de depuración remota.</span><span class="sxs-lookup"><span data-stu-id="8fc16-179">Set up two breaking points, and then select the **Debug** icon to start the remote debugging process.</span></span>

2. <span data-ttu-id="8fc16-180">El código se detiene en el primer punto de interrupción y se muestra la información de parámetros y variables en el panel **Variables**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-180">The code stops at the first breaking point, and the parameter and variable information are shown in the **Variables** pane.</span></span> 

3. <span data-ttu-id="8fc16-181">Seleccione el icono **Resume Program** (Continuar programa) para continuar.</span><span class="sxs-lookup"><span data-stu-id="8fc16-181">Select the **Resume Program** icon to continue.</span></span> <span data-ttu-id="8fc16-182">El código se detiene en el segundo punto.</span><span class="sxs-lookup"><span data-stu-id="8fc16-182">The code stops at the second point.</span></span> <span data-ttu-id="8fc16-183">La excepción se detecta según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="8fc16-183">The exception is caught as expected.</span></span>

  ![Iniciar error](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="8fc16-185">Vuelva a seleccionar el icono **Resume Program** (Continuar programa).</span><span class="sxs-lookup"><span data-stu-id="8fc16-185">Select the **Resume Program** icon again.</span></span> <span data-ttu-id="8fc16-186">La ventana **HDInsight Spark Subsmission**  (Envío de HDInsight Spark) muestra un error de ejecución de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8fc16-186">The **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Envío de error](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="8fc16-188">Para actualizar de forma dinámica el valor de variable mediante la funcionalidad de depuración de IntelliJ, vuelva a seleccionar **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-188">To dynamically update the variable value by using the IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="8fc16-189">El panel **Variables** aparece de nuevo.</span><span class="sxs-lookup"><span data-stu-id="8fc16-189">The **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="8fc16-190">Haga clic con el botón derecho en el destino en el pestaña **Depurar** y, a continuación, seleccione **Establecer valor**.</span><span class="sxs-lookup"><span data-stu-id="8fc16-190">Right-click the target on the **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="8fc16-191">Luego escriba un nuevo valor para la variable.</span><span class="sxs-lookup"><span data-stu-id="8fc16-191">Next, enter a new value for the variable.</span></span> <span data-ttu-id="8fc16-192">A continuación, seleccione **Entrar** para guardar el valor.</span><span class="sxs-lookup"><span data-stu-id="8fc16-192">Then select **Enter** to save the value.</span></span> 

  ![Establecer valor](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="8fc16-194">Seleccione el icono **Resume Program** (Continuar programa) para seguir ejecutando el programa.</span><span class="sxs-lookup"><span data-stu-id="8fc16-194">Select the **Resume Program** icon to continue to run the program.</span></span> <span data-ttu-id="8fc16-195">Esta vez no se detecta ninguna excepción.</span><span class="sxs-lookup"><span data-stu-id="8fc16-195">This time, no exception is caught.</span></span> <span data-ttu-id="8fc16-196">Puede ver que el proyecto se ejecuta correctamente sin ninguna excepción.</span><span class="sxs-lookup"><span data-stu-id="8fc16-196">You can see that the project runs successfully without any exceptions.</span></span>

  ![Depurar sin excepciones](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="8fc16-198"><a name="seealso"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8fc16-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="8fc16-199">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8fc16-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="8fc16-200">Demostración</span><span class="sxs-lookup"><span data-stu-id="8fc16-200">Demo</span></span>
* <span data-ttu-id="8fc16-201">Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="8fc16-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="8fc16-202">Depuración remota (vídeo): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster (Uso del Kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones Spark en un clúster de HDInsight)](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="8fc16-202">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="8fc16-203">Escenarios</span><span class="sxs-lookup"><span data-stu-id="8fc16-203">Scenarios</span></span>
* [<span data-ttu-id="8fc16-204">Spark con BI: realización del análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="8fc16-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8fc16-205">Spark con Machine Learning: uso de Spark en HDInsight para analizar la temperatura de edificios con los datos del sistema de acondicionamiento de aire</span><span class="sxs-lookup"><span data-stu-id="8fc16-205">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8fc16-206">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="8fc16-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8fc16-207">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="8fc16-207">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8fc16-208">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fc16-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8fc16-209">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8fc16-209">Create and run applications</span></span>
* [<span data-ttu-id="8fc16-210">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="8fc16-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8fc16-211">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="8fc16-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8fc16-212">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="8fc16-212">Tools and extensions</span></span>
* [<span data-ttu-id="8fc16-213">Uso del kit de herramientas de Azure para IntelliJ con el fin de crear aplicaciones Spark para un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fc16-213">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8fc16-214">Uso del kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones Spark mediante VPN</span><span class="sxs-lookup"><span data-stu-id="8fc16-214">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8fc16-215">Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="8fc16-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="8fc16-216">Uso de las herramientas de HDInsight del kit de herramientas de Azure para Eclipse con el fin de crear aplicaciones Spark</span><span class="sxs-lookup"><span data-stu-id="8fc16-216">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="8fc16-217">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fc16-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8fc16-218">Kernels para Jupyter Notebook en clústeres Spark en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fc16-218">Kernels available for Jupyter notebook in the Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8fc16-219">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="8fc16-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="8fc16-220">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8fc16-220">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="8fc16-221">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="8fc16-221">Manage resources</span></span>
* [<span data-ttu-id="8fc16-222">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="8fc16-222">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8fc16-223">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="8fc16-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
