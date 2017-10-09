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
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="726a8-103">Usar el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="726a8-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="726a8-104">Use Hola Kit de herramientas de Azure para aplicaciones de Spark de complemento toodevelop IntelliJ escritas en Scala y, a continuación, envíelos tooan clúster de HDInsight Spark directamente desde el entorno de desarrollo integrado de hello IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="726a8-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="726a8-105">Puede usar Hola complemento de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="726a8-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="726a8-106">Desarrollar y enviar una aplicación Spark en Scala en un clúster de Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="726a8-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="726a8-107">Tener acceso a los recursos del clúster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="726a8-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="726a8-108">Desarrollar y ejecutar localmente una aplicación Spark en Scala.</span><span class="sxs-lookup"><span data-stu-id="726a8-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="726a8-109">toocreate su proyecto, Hola vista [crear aplicaciones de Spark con hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) vídeo.</span><span class="sxs-lookup"><span data-stu-id="726a8-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="726a8-110">Puede usar este complemento toocreate y enviar solicitudes para un clúster de HDInsight Spark en Linux.</span><span class="sxs-lookup"><span data-stu-id="726a8-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="726a8-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="726a8-111">Prerequisites</span></span>

- <span data-ttu-id="726a8-112">Un clúster Apache Spark en HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="726a8-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="726a8-113">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="726a8-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="726a8-114">Kit de desarrollo de Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="726a8-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="726a8-115">Puede instalarlo desde hello [sitio Web de Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="726a8-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="726a8-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="726a8-116">IntelliJ IDEA.</span></span> <span data-ttu-id="726a8-117">En este artículo se usa la versión 2017.1.</span><span class="sxs-lookup"><span data-stu-id="726a8-117">This article uses version 2017.1.</span></span> <span data-ttu-id="726a8-118">Puede instalarlo desde hello [sitio Web de JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="726a8-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="726a8-119">Instalación del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="726a8-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="726a8-120">Para obtener instrucciones de instalación, consulte [Instalación del kit de herramientas de Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="726a8-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="726a8-121">Inicie sesión en tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="726a8-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="726a8-122">Iniciar hello IntelliJ IDE y abra el Explorador de Azure.</span><span class="sxs-lookup"><span data-stu-id="726a8-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="726a8-123">En hello **vista** menú, seleccione **las ventanas de herramientas**y, a continuación, seleccione **explorador Azure**.</span><span class="sxs-lookup"><span data-stu-id="726a8-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![vínculo de explorador Azure Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="726a8-125">Menú contextual hello **Azure** nodo y, a continuación, seleccione **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="726a8-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="726a8-126">Hola **inicio de sesión en Azure** cuadro de diálogo, seleccione **iniciar sesión en**y, a continuación, escriba sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="726a8-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![cuadro de Hello Azure inicio de sesión de diálogo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="726a8-128">Después de que ha iniciado sesión, Hola **seleccione suscripciones** Hola a todos Hola suscripciones de Azure que están asociadas con el cuadro de diálogo enumera las credenciales.</span><span class="sxs-lookup"><span data-stu-id="726a8-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="726a8-129">Seleccione hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="726a8-129">Select hello **Select** button.</span></span>

    ![cuadro de diálogo Seleccionar suscripciones Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="726a8-131">En hello **explorador Azure** , expanda **HDInsight** tooview Hola clústeres de HDInsight Spark y que se encuentran en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="726a8-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Clústeres de HDInsight Spark en Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="726a8-133">tooview Hola recursos (por ejemplo, cuentas de almacenamiento) que están asociados con el clúster de hello, expandir un nodo de nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="726a8-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Nodo de nombre de clúster expandido](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="726a8-135">Ejecución de una aplicación Spark en Scala en un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="726a8-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="726a8-136">Inicie IntelliJ IDEA y, después, cree un proyecto.</span><span class="sxs-lookup"><span data-stu-id="726a8-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="726a8-137">Hola **nuevo proyecto** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="726a8-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="726a8-138">a.</span><span class="sxs-lookup"><span data-stu-id="726a8-138">a.</span></span> <span data-ttu-id="726a8-139">Seleccione **HDInsight** > **Spark en HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="726a8-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="726a8-140">b.</span><span class="sxs-lookup"><span data-stu-id="726a8-140">b.</span></span> <span data-ttu-id="726a8-141">Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:</span><span class="sxs-lookup"><span data-stu-id="726a8-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="726a8-142">**Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="726a8-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="726a8-143">**SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola</span><span class="sxs-lookup"><span data-stu-id="726a8-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="726a8-145">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="726a8-145">Select **Next**.</span></span>

3. <span data-ttu-id="726a8-146">Asistente para la creación del proyecto de Hello Scala detecta automáticamente si ha instalado Hola Scala complemento.</span><span class="sxs-lookup"><span data-stu-id="726a8-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="726a8-147">Seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-147">Select **Install**.</span></span>

   ![Comprobación de complemento de Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="726a8-149">Hola toodownload Scala complemento, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="726a8-150">Siga las instrucciones de hello toorestart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="726a8-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![cuadro de diálogo de instalación de complemento de Hello Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="726a8-152">Hola **nuevo proyecto** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="726a8-152">In hello **New Project** window, do hello following:</span></span>  

    ![Seleccionar Hola Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="726a8-154">a.</span><span class="sxs-lookup"><span data-stu-id="726a8-154">a.</span></span> <span data-ttu-id="726a8-155">Escriba un nombre y una ubicación de proyecto.</span><span class="sxs-lookup"><span data-stu-id="726a8-155">Enter a project name and location.</span></span>

   <span data-ttu-id="726a8-156">b.</span><span class="sxs-lookup"><span data-stu-id="726a8-156">b.</span></span> <span data-ttu-id="726a8-157">Hola **proyecto SDK** lista desplegable, seleccione **Java 1.8** para clúster de hello Spark 2.x, o bien seleccione **Java 1.7** para clúster de hello Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="726a8-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="726a8-158">c.</span><span class="sxs-lookup"><span data-stu-id="726a8-158">c.</span></span> <span data-ttu-id="726a8-159">Hola **versión Spark** lista desplegable, el Asistente para crear un proyecto Scala integra con la versión adecuada de Hola de SDK de Spark y Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="726a8-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="726a8-160">Si la versión de clúster de Spark hello es anterior a la 2.0, seleccione **inspirará 1.x**.</span><span class="sxs-lookup"><span data-stu-id="726a8-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="726a8-161">De lo contrario, seleccione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="726a8-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="726a8-162">Este ejemplo utiliza **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="726a8-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="726a8-163">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-163">Select **Finish**.</span></span>

7. <span data-ttu-id="726a8-164">proyecto de Spark Hola crea automáticamente un artefacto por usted.</span><span class="sxs-lookup"><span data-stu-id="726a8-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="726a8-165">artefacto de hello tooview, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="726a8-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="726a8-166">a.</span><span class="sxs-lookup"><span data-stu-id="726a8-166">a.</span></span> <span data-ttu-id="726a8-167">En hello **archivo** menú, seleccione **estructura del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="726a8-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="726a8-168">b.</span><span class="sxs-lookup"><span data-stu-id="726a8-168">b.</span></span> <span data-ttu-id="726a8-169">Hola **estructura del proyecto** cuadro de diálogo, seleccione **artefactos** artefacto de predeterminado de hello tooview que se crea.</span><span class="sxs-lookup"><span data-stu-id="726a8-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="726a8-170">También puede crear su propios artefacto seleccionando el signo más hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="726a8-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Información de artefacto en el cuadro de diálogo de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="726a8-172">Agregue el código fuente de aplicación haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="726a8-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="726a8-173">a.</span><span class="sxs-lookup"><span data-stu-id="726a8-173">a.</span></span> <span data-ttu-id="726a8-174">En el Explorador de proyectos, haga clic en **src**, seleccione demasiado**New**y, a continuación, seleccione **Scala clase**.</span><span class="sxs-lookup"><span data-stu-id="726a8-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Comandos para crear una clase Scala desde el explorador de proyectos](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="726a8-176">b.</span><span class="sxs-lookup"><span data-stu-id="726a8-176">b.</span></span> <span data-ttu-id="726a8-177">Hola **crear nueva clase Scala** diálogo cuadro, proporcione un nombre, seleccione **objeto** en hello **tipo** cuadro y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Creación de un cuadro de diálogo de nueva clase de Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="726a8-179">c.</span><span class="sxs-lookup"><span data-stu-id="726a8-179">c.</span></span> <span data-ttu-id="726a8-180">Hola **MyClusterApp.scala** de archivo, pegue el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="726a8-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="726a8-181">Hello código lee los datos de Hola de HVAC.csv (disponible en todos los clústeres de HDInsight Spark), se recuperan las filas de Hola que sólo tienen un dígito en la columna séptimo hello en el archivo CSV de Hola y escribe la salida de hello demasiado**/HVACOut** en el valor predeterminado de Hola contenedor de almacenamiento de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

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

9. <span data-ttu-id="726a8-182">Ejecutar la aplicación hello en un clúster de HDInsight Spark haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="726a8-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="726a8-183">a.</span><span class="sxs-lookup"><span data-stu-id="726a8-183">a.</span></span> <span data-ttu-id="726a8-184">En el Explorador de proyectos, haga clic en el nombre del proyecto de Hola y, a continuación, seleccione **tooHDInsight enviar Spark aplicación**.</span><span class="sxs-lookup"><span data-stu-id="726a8-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![comando de tooHDInsight enviar Spark aplicación Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="726a8-186">b.</span><span class="sxs-lookup"><span data-stu-id="726a8-186">b.</span></span> <span data-ttu-id="726a8-187">Se está tooenter solicitada sus credenciales de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="726a8-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="726a8-188">Hola **Spark envío** cuadro de diálogo, proporcione Hola después de valores y, a continuación, seleccione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="726a8-189">Para **inspirará clústeres (solamente para Linux)**, seleccione Hola clúster de HDInsight Spark en el que desea que toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="726a8-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="726a8-190">Seleccione un artefacto hello IntelliJ proyecto o seleccione uno de la unidad de disco duro de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="726a8-191">Hola **nombre de la clase principal** cuadro de puntos suspensivos de hello seleccione (**...** ), seleccione la clase principal de hello en el código fuente de aplicación y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![cuadro de diálogo Seleccionar clase de Main Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="726a8-193">Porque no requiere argumentos de línea de comandos o no hacer referencia a archivos JAR o archivos de código de la aplicación hello en este ejemplo, puede dejar Hola restantes cuadros vacíos.</span><span class="sxs-lookup"><span data-stu-id="726a8-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="726a8-194">Después de proporcionar toda la información de hello, cuadro de diálogo de hello debe ser similar a Hola después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="726a8-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![cuadro de diálogo de envío de Spark Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="726a8-196">c.</span><span class="sxs-lookup"><span data-stu-id="726a8-196">c.</span></span> <span data-ttu-id="726a8-197">Hola **Spark envío** ficha situada en la parte inferior de Hola de ventana hello debe comenzar a mostrar el progreso de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="726a8-198">También puede detener la aplicación hello seleccionando botón rojo Hola Hola **Spark envío** ventana.</span><span class="sxs-lookup"><span data-stu-id="726a8-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![ventana de envío de Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="726a8-200">toolearn cómo tooaccess Hola salida del trabajo, vea Hola "acceso y administrar clústeres de HDInsight Spark mediante el Kit de herramientas de Azure para IntelliJ" sección más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="726a8-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="726a8-201">Ejecución o depuración de una aplicación Spark en Scala en un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="726a8-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="726a8-202">También se recomienda otra forma de enviar el clúster de hello Spark application toohello.</span><span class="sxs-lookup"><span data-stu-id="726a8-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="726a8-203">Puede hacerlo estableciendo los parámetros de Hola Hola **las configuraciones de ejecución y depuración** IDE.</span><span class="sxs-lookup"><span data-stu-id="726a8-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="726a8-204">Para obtener más información, consulte [Depuración de aplicaciones de Spark de forma remota en un clúster de HDInsight con el kit de herramientas de Azure para IntelliJ mediante SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="726a8-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="726a8-205">Acceso y administración de clústeres de HDInsight Spark mediante el uso del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="726a8-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="726a8-206">Puede realizar varias operaciones mediante el Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="726a8-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="726a8-207">Vista de trabajos de Hola de acceso</span><span class="sxs-lookup"><span data-stu-id="726a8-207">Access hello job view</span></span>
1. <span data-ttu-id="726a8-208">En el Explorador de Azure, expanda **HDInsight**, expanda el nombre del clúster de Spark hello y, a continuación, seleccione **trabajos**.</span><span class="sxs-lookup"><span data-stu-id="726a8-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Nodo Vista de trabajos](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="726a8-210">En el panel derecho de hello, Hola **Spark trabajo vista** ficha muestra todas las aplicaciones de Hola que se ejecutaron en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="726a8-211">Seleccione el nombre de Hola de aplicación hello para el que desea toosee más detalles.</span><span class="sxs-lookup"><span data-stu-id="726a8-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![Detalles de aplicación](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="726a8-213">toodisplay ejecución trabajo información básica, mantenga el mouse sobre el gráfico de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="726a8-214">gráfico de fases de hello tooview y la información que genera cada trabajo, seleccione un nodo en el gráfico de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![Detalles de fase de trabajo](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="726a8-216">tooview utilizados con frecuencia los registros, como *controlador Stderr*, *controlador Stdout*, y *información de directorio*, seleccione hello **registro** ficha.</span><span class="sxs-lookup"><span data-stu-id="726a8-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Detalles del registro](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="726a8-218">También puede ver Hola historial Spark interfaz de usuario y hello YARN interfaz de usuario (en el nivel de aplicación Hola) seleccionando un vínculo en la parte superior de Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="726a8-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="726a8-219">Servidor de acceso Hola Spark historial</span><span class="sxs-lookup"><span data-stu-id="726a8-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="726a8-220">En Azure Explorer, expanda **HDInsight**, haga clic con el botón derecho en el nombre del clúster de Spark y seleccione **Open Spark History UI** (Abrir IU de historial de Spark).</span><span class="sxs-lookup"><span data-stu-id="726a8-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="726a8-221">Cuando se le pida, escriba credenciales de administrador del clúster de hello, que especificó al configurar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="726a8-222">En el panel del servidor de hello Spark historial, puede usar toolook de nombre de aplicación Hola para aplicación Hola que simplemente terminado de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="726a8-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="726a8-223">En el anterior código de hello, establecer nombre de la aplicación hello mediante `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="726a8-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="726a8-224">Por lo tanto, el nombre de aplicación Spark es **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="726a8-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="726a8-225">Iniciar hello Ambari portal</span><span class="sxs-lookup"><span data-stu-id="726a8-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="726a8-226">En Azure Explorer, expanda **HDInsight**, haga clic con el botón derecho en el nombre del clúster de Spark y seleccione **Open Cluster Management Portal (Ambari)** (Abrir el portal de administración de clústeres [Ambari]).</span><span class="sxs-lookup"><span data-stu-id="726a8-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="726a8-227">Cuando se le pida, escriba las credenciales de administrador de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="726a8-228">Estas credenciales se especificó durante el proceso de instalación de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="726a8-229">Administración de suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="726a8-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="726a8-230">De forma predeterminada, Azure Toolkit for IntelliJ enumera los clústeres de Spark Hola de todas las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="726a8-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="726a8-231">Si es necesario, puede especificar las suscripciones de Hola que desea tooaccess.</span><span class="sxs-lookup"><span data-stu-id="726a8-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="726a8-232">En el Explorador de Azure, haga clic en hello **Azure** nodo raíz y, a continuación, seleccione **administrar suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="726a8-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="726a8-233">En el cuadro de diálogo de hello, desactive Hola casillas de verificación siguiente toohello las suscripciones que no desee tooaccess y, a continuación, seleccione **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="726a8-234">También puede seleccionar **cerrar sesión** si desea toosign fuera de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="726a8-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="726a8-235">Ejecución local de una aplicación Spark en Scala</span><span class="sxs-lookup"><span data-stu-id="726a8-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="726a8-236">Puede usar el Kit de herramientas de Azure para aplicaciones de IntelliJ toorun Spark Scala localmente en la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="726a8-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="726a8-237">Hola aplicaciones normalmente no necesita tener acceso a recursos de toocluster, como contenedores de almacenamiento, y se puede ejecutar y se prueban localmente.</span><span class="sxs-lookup"><span data-stu-id="726a8-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="726a8-238">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="726a8-238">Prerequisite</span></span>
<span data-ttu-id="726a8-239">Mientras se ejecuta la aplicación local de Spark Scala de hello en un equipo Windows, podría obtener una excepción, como se explica en [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="726a8-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="726a8-240">excepción de Hola se produce porque falta WinUtils.exe en Windows.</span><span class="sxs-lookup"><span data-stu-id="726a8-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="726a8-241">tooresolve este error, [descargar ejecutable hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa ubicación como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="726a8-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="726a8-242">A continuación, agregue la variable de entorno de hello **HADOOP_HOME**y establezca el valor de Hola de variable de hello demasiado**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="726a8-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="726a8-243">Ejecución de una aplicación Spark en Scala local</span><span class="sxs-lookup"><span data-stu-id="726a8-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="726a8-244">Inicie IntelliJ IDEA y cree un proyecto.</span><span class="sxs-lookup"><span data-stu-id="726a8-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="726a8-245">Hola **nuevo proyecto** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="726a8-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="726a8-246">a.</span><span class="sxs-lookup"><span data-stu-id="726a8-246">a.</span></span> <span data-ttu-id="726a8-247">Seleccione **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Ejemplo de ejecución local de Spark en HDInsight [Scala]).</span><span class="sxs-lookup"><span data-stu-id="726a8-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="726a8-248">b.</span><span class="sxs-lookup"><span data-stu-id="726a8-248">b.</span></span> <span data-ttu-id="726a8-249">Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:</span><span class="sxs-lookup"><span data-stu-id="726a8-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="726a8-250">**Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="726a8-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="726a8-251">**SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola</span><span class="sxs-lookup"><span data-stu-id="726a8-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="726a8-253">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="726a8-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="726a8-254">En la siguiente ventana de Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="726a8-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="726a8-255">a.</span><span class="sxs-lookup"><span data-stu-id="726a8-255">a.</span></span> <span data-ttu-id="726a8-256">Escriba un nombre y una ubicación de proyecto.</span><span class="sxs-lookup"><span data-stu-id="726a8-256">Enter a project name and location.</span></span>

    <span data-ttu-id="726a8-257">b.</span><span class="sxs-lookup"><span data-stu-id="726a8-257">b.</span></span> <span data-ttu-id="726a8-258">Hola **proyecto SDK** lista desplegable, seleccione una versión de Java que es posterior a la versión 1.7.</span><span class="sxs-lookup"><span data-stu-id="726a8-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="726a8-259">c.</span><span class="sxs-lookup"><span data-stu-id="726a8-259">c.</span></span> <span data-ttu-id="726a8-260">Hola **versión Spark** lista desplegable, versión de Hola select de Scala que desea toouse: Scala 2.11.x para Spark 2.0 o Scala 2.10.x para Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="726a8-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="726a8-262">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="726a8-262">Select **Finish**.</span></span>

6. <span data-ttu-id="726a8-263">plantilla de Hello agrega un código de ejemplo (**LogQuery**) en hello **src** carpeta que puede ejecutar localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="726a8-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Ubicación de LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="726a8-265">Menú contextual hello **LogQuery** aplicación y, a continuación, seleccione **ejecución 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="726a8-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="726a8-266">En hello **ejecutar** ficha en la parte inferior de hello, verá una salida como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="726a8-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Resultado de la ejecución local de la aplicación Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="726a8-268">Convertir existente IntelliJ IDEA aplicaciones toouse Kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="726a8-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="726a8-269">Puede convertir Hola Spark Scala las aplicaciones existentes que ha creado en la IDEA de IntelliJ toobe compatible con el Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="726a8-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="726a8-270">A continuación, puede usar hello toosubmit complemento Hola aplicaciones tooan clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="726a8-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="726a8-271">Para una aplicación de Spark Scala existente que se creó a través de la IDEA de IntelliJ, abra el archivo de .iml asociados de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="726a8-272">En la raíz de hello nivel es un **módulo** elemento como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="726a8-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="726a8-273">Editar Hola elemento tooadd `UniqueKey="HDInsightTool"` así que Hola **módulo** elemento aspecto Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="726a8-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="726a8-274">Guarde los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="726a8-274">Save hello changes.</span></span> <span data-ttu-id="726a8-275">La aplicación ahora debe ser compatible con el kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="726a8-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="726a8-276">Se puede probar haciendo clic en el nombre del proyecto hello en el Explorador de proyectos.</span><span class="sxs-lookup"><span data-stu-id="726a8-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="726a8-277">menú emergente de Hello ahora tiene la opción de hello **tooHDInsight enviar Spark aplicación**.</span><span class="sxs-lookup"><span data-stu-id="726a8-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="726a8-278">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="726a8-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="726a8-279">Error en la ejecución local: *Please use a larger heap size* (Utilice un tamaño de montón mayor)</span><span class="sxs-lookup"><span data-stu-id="726a8-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="726a8-280">En Spark 1.6, si usas un SDK de Java de 32 bits durante la ejecución local, podría encontrar Hola siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="726a8-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

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

<span data-ttu-id="726a8-281">Estos errores tienen lugar porque el tamaño del montón de hello no es lo suficientemente grande como para toorun Spark.</span><span class="sxs-lookup"><span data-stu-id="726a8-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="726a8-282">Spark requiere al menos 471 MB.</span><span class="sxs-lookup"><span data-stu-id="726a8-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="726a8-283">(para obtener más información, consulte [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081)). Una solución simple es toouse un SDK de Java de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="726a8-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="726a8-284">También puede cambiar la configuración de JVM hello en IntelliJ agregando Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="726a8-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Agregar opciones toohello "Opciones de VM" cuadro IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="726a8-286">P+F</span><span class="sxs-lookup"><span data-stu-id="726a8-286">FAQ</span></span>
<span data-ttu-id="726a8-287">elegir un almacén de aplicación tooAzure Data Lake, toosubmit **Interactive** modo durante el proceso de Hola de inicio de sesión Azure.</span><span class="sxs-lookup"><span data-stu-id="726a8-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="726a8-288">Si selecciona el modo **Automatizado**, puede aparecer un error.</span><span class="sxs-lookup"><span data-stu-id="726a8-288">If you select **Automated** mode, you can get an error.</span></span>

![inicio de sesión interactivo](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="726a8-290">Ahora se ha resuelto.</span><span class="sxs-lookup"><span data-stu-id="726a8-290">Now, we resolved it.</span></span> <span data-ttu-id="726a8-291">Puede elegir la aplicación de un clúster de Azure datos Lake toosubmit con cualquier método de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="726a8-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="726a8-292">Comentarios y problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="726a8-292">Feedback and known issues</span></span>
<span data-ttu-id="726a8-293">Actualmente, la visualización de salidas de Spark directamente no se admite.</span><span class="sxs-lookup"><span data-stu-id="726a8-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="726a8-294">Si tiene sugerencias o comentarios, o si se le presenta algún problema al usar este complemento, no dude en enviarnos un correo electrónico a la dirección hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="726a8-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="726a8-295"><a name="seealso"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="726a8-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="726a8-296">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="726a8-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="726a8-297">Demostración</span><span class="sxs-lookup"><span data-stu-id="726a8-297">Demo</span></span>
* <span data-ttu-id="726a8-298">Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="726a8-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="726a8-299">Depuración remota (vídeo): [Use Azure Toolkit IntelliJ toodebug Spark para aplicaciones de forma remota en clúster de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="726a8-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="726a8-300">Escenarios</span><span class="sxs-lookup"><span data-stu-id="726a8-300">Scenarios</span></span>
* [<span data-ttu-id="726a8-301">Spark con BI: realización del análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="726a8-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="726a8-302">Spark con aprendizaje automático: Use Spark en tooanalyze HDInsight generar temperatura utilizando los datos HVAC</span><span class="sxs-lookup"><span data-stu-id="726a8-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="726a8-303">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="726a8-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="726a8-304">La transmisión por secuencias Spark: Use Spark en HDInsight toobuild aplicaciones de transmisión por secuencias en tiempo real</span><span class="sxs-lookup"><span data-stu-id="726a8-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="726a8-305">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="726a8-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="726a8-306">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="726a8-306">Creating and running applications</span></span>
* [<span data-ttu-id="726a8-307">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="726a8-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="726a8-308">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="726a8-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="726a8-309">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="726a8-309">Tools and extensions</span></span>
* [<span data-ttu-id="726a8-310">Usar el Kit de herramientas de Azure para las aplicaciones de IntelliJ toodebug Spark forma remota a través de VPN</span><span class="sxs-lookup"><span data-stu-id="726a8-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="726a8-311">Usar el Kit de herramientas de Azure para aplicaciones de Spark IntelliJ toodebug forma remota a través de SSH</span><span class="sxs-lookup"><span data-stu-id="726a8-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="726a8-312">Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="726a8-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="726a8-313">Usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark</span><span class="sxs-lookup"><span data-stu-id="726a8-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="726a8-314">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="726a8-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="726a8-315">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="726a8-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="726a8-316">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="726a8-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="726a8-317">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="726a8-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="726a8-318">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="726a8-318">Managing resources</span></span>
* [<span data-ttu-id="726a8-319">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="726a8-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="726a8-320">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="726a8-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

