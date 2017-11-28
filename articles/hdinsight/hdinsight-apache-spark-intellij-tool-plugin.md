---
title: "Kit de herramientas de Azure para IntelliJ: creación de aplicaciones Spark para un clúster de HDInsight | Microsoft Docs"
description: "Uso del kit de herramientas de Azure para IntelliJ con el fin de desarrollar aplicaciones Spark escritas en Scala y enviarlas a un clúster de HDInsight Spark."
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="c0a5d-103">Uso del kit de herramientas de Azure para IntelliJ con el fin de crear aplicaciones Spark para un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0a5d-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="c0a5d-104">Uso del complemento de kit de herramientas de Azure para IntelliJ con el fin de desarrollar aplicaciones Spark escritas en Scala y enviarlas a continuación a un clúster de HDInsight Spark directamente desde el entorno de desarrollo integrado (IDE) de IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="c0a5d-105">Puede usar el complemento de varias maneras:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="c0a5d-106">Desarrollar y enviar una aplicación Spark en Scala en un clúster de Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="c0a5d-107">Tener acceso a los recursos del clúster de Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="c0a5d-108">Desarrollar y ejecutar localmente una aplicación Spark en Scala.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="c0a5d-109">Para crear el proyecto, vea el vídeo [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (Creación de aplicaciones Spark con el kit de herramientas de Azure para IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0a5d-110">Puede usar este complemento para crear y enviar aplicaciones solo para un clúster de HDInsight Spark en Linux.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="c0a5d-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c0a5d-111">Prerequisites</span></span>

- <span data-ttu-id="c0a5d-112">Un clúster Apache Spark en HDInsight Linux.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="c0a5d-113">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="c0a5d-114">Kit de desarrollo de Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="c0a5d-115">Puede instalarlo desde el [sitio web de Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="c0a5d-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-116">IntelliJ IDEA.</span></span> <span data-ttu-id="c0a5d-117">En este artículo se usa la versión 2017.1.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-117">This article uses version 2017.1.</span></span> <span data-ttu-id="c0a5d-118">Puede instalarlo desde el [sitio web de JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="c0a5d-119">Instalación del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c0a5d-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="c0a5d-120">Para obtener instrucciones de instalación, consulte [Instalación del kit de herramientas de Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="c0a5d-121">Inicie sesión en la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="c0a5d-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="c0a5d-122">Inicie el IDE de IntelliJ y abra Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="c0a5d-123">En el menú **View** (Ver), seleccione **Tools Windows** (Ventanas de herramientas) y luego seleccione **Azure Explorer** (Explorador de Azure).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![Vínculo de Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="c0a5d-125">Haga clic con el botón derecho en el nodo **Azure** y después seleccione **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="c0a5d-126">En el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Iniciar sesión** y, a continuación, escriba las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Cuadro de diálogo de inicio de sesión en Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="c0a5d-128">Cuando haya iniciado sesión, en el cuadro de diálogo **Select Subscriptions** (Seleccionar suscripciones) se enumeran todas las suscripciones de Azure asociadas a las credenciales.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="c0a5d-129">Seleccione el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-129">Select the **Select** button.</span></span>

    ![Cuadro de diálogo Seleccionar suscripciones](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="c0a5d-131">En la pestaña **Azure Explorer**, expanda **HDInsight** para ver los clústeres de HDInsight Spark de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Clústeres de HDInsight Spark en Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="c0a5d-133">Para ver los recursos (por ejemplo, las cuentas de almacenamiento) asociados al clúster, puede expandir un nodo de nombre de clúster.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![Nodo de nombre de clúster expandido](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="c0a5d-135">Ejecución de una aplicación Spark en Scala en un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="c0a5d-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="c0a5d-136">Inicie IntelliJ IDEA y, después, cree un proyecto.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="c0a5d-137">En el cuadro de diálogo **Nuevo proyecto** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="c0a5d-138">a.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-138">a.</span></span> <span data-ttu-id="c0a5d-139">Seleccione **HDInsight** > **Spark en HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="c0a5d-140">b.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-140">b.</span></span> <span data-ttu-id="c0a5d-141">En la lista de **herramientas de compilación**, seleccione cualquiera de las siguientes, según sus necesidades:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="c0a5d-142">**Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="c0a5d-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="c0a5d-143">**SBT**, para administrar las dependencias y compilar el proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="c0a5d-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Cuadro de diálogo Nuevo proyecto](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="c0a5d-145">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-145">Select **Next**.</span></span>

3. <span data-ttu-id="c0a5d-146">El asistente para crear un proyecto de Scala detecta automáticamente si se ha instalado el complemento de Scala.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="c0a5d-147">Seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-147">Select **Install**.</span></span>

   ![Comprobación de complemento de Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="c0a5d-149">Para descargar el complemento de Scala, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="c0a5d-150">Siga las instrucciones para reiniciar IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![Cuadro de diálogo de instalación del complemento de Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="c0a5d-152">En la ventana **Nuevo proyecto**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-152">In the **New Project** window, do the following:</span></span>  

    ![Selección del SDK de Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="c0a5d-154">a.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-154">a.</span></span> <span data-ttu-id="c0a5d-155">Escriba un nombre y una ubicación de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-155">Enter a project name and location.</span></span>

   <span data-ttu-id="c0a5d-156">b.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-156">b.</span></span> <span data-ttu-id="c0a5d-157">En la lista desplegable **SDK de proyecto**, seleccione **Java 1.8** para el clúster Spark 2.x, o bien **Java 1.7** para el clúster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="c0a5d-158">c.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-158">c.</span></span> <span data-ttu-id="c0a5d-159">En la lista desplegable **Versión de Spark**, el asistente para crear un proyecto de Scala integra la versión correcta del SDK de Spark y el SDK de Scala.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="c0a5d-160">Si la versión del clúster de Spark es inferior a la 2.0, seleccione **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="c0a5d-161">De lo contrario, seleccione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="c0a5d-162">Este ejemplo utiliza **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="c0a5d-163">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-163">Select **Finish**.</span></span>

7. <span data-ttu-id="c0a5d-164">El proyecto Spark creará automáticamente un artefacto.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="c0a5d-165">Para ver el artefacto, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="c0a5d-166">a.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-166">a.</span></span> <span data-ttu-id="c0a5d-167">En el menú **File** (Archivo), seleccione **Project Structure** (Estructura del proyecto).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="c0a5d-168">b.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-168">b.</span></span> <span data-ttu-id="c0a5d-169">En el cuadro de diálogo **Project Structure** (Estructura del proyecto), seleccione **Artifacts** (Artefactos) para ver el artefacto predeterminado que se crea.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="c0a5d-170">También puede crear su propio artefacto seleccionando el signo más (**+**).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![Información de artefacto en el cuadro de diálogo](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="c0a5d-172">Agregue el código fuente de aplicación de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="c0a5d-173">a.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-173">a.</span></span> <span data-ttu-id="c0a5d-174">En el Explorador de proyectos, haga clic con el botón derecho en **src**, elija **New** (Nuevo) y, a continuación, seleccione **Scala Class** (Clase de Scala).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![Comandos para crear una clase Scala desde el explorador de proyectos](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="c0a5d-176">b.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-176">b.</span></span> <span data-ttu-id="c0a5d-177">En el cuadro de diálogo **Create New Scala Class** (Crear nueva clase de Scala), proporcione un nombre, seleccione **Object** (Objeto) en **Kind** (Variante) y seleccione **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![Creación de un cuadro de diálogo de nueva clase de Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="c0a5d-179">c.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-179">c.</span></span> <span data-ttu-id="c0a5d-180">En el archivo **MyClusterApp.scala** , pegue el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="c0a5d-181">El código lee los datos de HVAC.csv (disponible en todos los clústeres de HDInsight Spark), recupera las filas que solo tienen un dígito en la séptima columna del archivo CSV y escribe la salida en **/HVACOut** en el contenedor de almacenamiento predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="c0a5d-182">Ejecute la aplicación en un clúster de HDInsight Spark de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="c0a5d-183">a.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-183">a.</span></span> <span data-ttu-id="c0a5d-184">En el explorador de proyectos, haga clic con el botón derecho en el nombre del proyecto y seleccione **Submit Spark Application to HDInsight** (Enviar aplicación Spark a HDInsight).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![Envío de aplicación Spark a comando HDInsight](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="c0a5d-186">b.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-186">b.</span></span> <span data-ttu-id="c0a5d-187">Se le pedirá que escriba las credenciales de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="c0a5d-188">En el cuadro de diálogo **Spark Submission** (Envío de Spark), proporcione los siguientes valores y luego seleccione **Submit** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="c0a5d-189">Para **Spark clusters (Linux only)**(Clústeres de Spark [solo Linux]), seleccione el clúster de Spark de HDInsight en el que desea ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="c0a5d-190">Seleccione un artefacto del proyecto IntelliJ o uno del disco duro.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="c0a5d-191">En el cuadro de texto **Main class name** (Nombre de clase principal), seleccione los puntos suspensivos (**ellipsis**), seleccione la clase principal del código fuente de aplicación y seleccione **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![Cuadro de diálogo de selección de clase principal](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="c0a5d-193">Dado que el código de aplicación de este ejemplo no requiere argumentos de línea de comandos ni archivos o JAR de referencia, puede dejar vacíos los demás cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="c0a5d-194">Después de proporcionar toda la información, el cuadro de diálogo debería parecerse a la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![Cuadro de diálogo de envío de Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="c0a5d-196">c.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-196">c.</span></span> <span data-ttu-id="c0a5d-197">La pestaña **Spark Submission** (Envío de Spark) de la parte inferior de la ventana debe empezar a mostrar el progreso.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="c0a5d-198">También puede detener la aplicación seleccionando el botón rojo en la ventana **Spark Submission** (Envío de Spark).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![Ventana de envío de Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="c0a5d-200">Para obtener información sobre cómo tener acceso a la salida de trabajo, consulte la sección "Acceso y administración de clústeres de HDInsight Spark mediante el uso del kit de herramientas de Azure para IntelliJ" que encontrará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="c0a5d-201">Ejecución o depuración de una aplicación Spark en Scala en un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="c0a5d-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="c0a5d-202">También se recomienda otra manera de enviar la aplicación Spark al clúster.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="c0a5d-203">Puede hacerlo estableciendo los parámetros del IDE de **configuraciones de ejecución o depuración**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="c0a5d-204">Para obtener más información, consulte [Depuración de aplicaciones de Spark de forma remota en un clúster de HDInsight con el kit de herramientas de Azure para IntelliJ mediante SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="c0a5d-205">Acceso y administración de clústeres de HDInsight Spark mediante el uso del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c0a5d-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="c0a5d-206">Puede realizar varias operaciones mediante el Kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="c0a5d-207">Acceso a la vista de trabajo</span><span class="sxs-lookup"><span data-stu-id="c0a5d-207">Access the job view</span></span>
1. <span data-ttu-id="c0a5d-208">En Azure Explorer, expanda **HDInsight** y el nombre del clúster de Spark. Después, seleccione **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![Nodo Vista de trabajos](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="c0a5d-210">En el panel derecho, la pestaña **Spark Job View** (Vista de trabajos de Spark) muestra todas las aplicaciones que se ejecutaron en el clúster.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="c0a5d-211">Seleccione el nombre de la aplicación para la que desea ver más detalles.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-211">Select the name of the application for which you want to see more details.</span></span>

    ![Detalles de aplicación](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="c0a5d-213">Para mostrar información básica del trabajo de ejecución, mantenga el mouse sobre el gráfico del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="c0a5d-214">Para ver el gráfico de fases y la información que todo trabajo genera, seleccione un nodo del gráfico del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![Detalles de fase de trabajo](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="c0a5d-216">Para ver registros usados con frecuencia, como *Driver Stderr*, *Driver Stdout* y *Directory Info*, seleccione la pestaña **Registro**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![Detalles del registro](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="c0a5d-218">También puede ver Spark History UI (IU de historial de Spark) y YARN UI (IU de YARN), en el nivel de aplicación, al seleccionar los vínculos correspondientes de la parte superior de la ventana.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="c0a5d-219">Acceso al servidor de historial de Spark</span><span class="sxs-lookup"><span data-stu-id="c0a5d-219">Access the Spark history server</span></span>
1. <span data-ttu-id="c0a5d-220">En Azure Explorer, expanda **HDInsight**, haga clic con el botón derecho en el nombre del clúster de Spark y seleccione **Open Spark History UI** (Abrir IU de historial de Spark).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="c0a5d-221">Cuando se le solicite, escriba las credenciales de administrador del clúster, que especificó al configurar el clúster.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="c0a5d-222">En el panel del servidor de historial de Spark, puede usar el nombre de aplicación para buscar la aplicación que acaba de terminar de ejecutar.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="c0a5d-223">En el código anterior, se establece el nombre de la aplicación mediante `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="c0a5d-224">Por lo tanto, el nombre de aplicación Spark es **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="c0a5d-225">Inicio del portal de Ambari</span><span class="sxs-lookup"><span data-stu-id="c0a5d-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="c0a5d-226">En Azure Explorer, expanda **HDInsight**, haga clic con el botón derecho en el nombre del clúster de Spark y seleccione **Open Cluster Management Portal (Ambari)** (Abrir el portal de administración de clústeres [Ambari]).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="c0a5d-227">Cuando se le pida, escriba las credenciales de administrador para el clúster.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="c0a5d-228">Estas son las credenciales que especificó durante el proceso de configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="c0a5d-229">Administración de suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c0a5d-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="c0a5d-230">De forma predeterminada, el kit de herramientas de Azure para IntelliJ enumera los clústeres de Spark de todas las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="c0a5d-231">Si es necesario, puede especificar las suscripciones a las que desea tener acceso.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="c0a5d-232">En Azure Explorer, haga clic con el botón derecho en el nodo raíz de **Azure** y seleccione **Manage Subscriptions** (Administrar suscripciones).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="c0a5d-233">En el cuadro de diálogo, desactive las casillas situadas junto a las suscripciones a las que no desea tener acceso y seleccione **Close** (Cerrar).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="c0a5d-234">También puede seleccionar **Sign Out** (Cerrar sesión) si desea cerrar sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="c0a5d-235">Ejecución local de una aplicación Spark en Scala</span><span class="sxs-lookup"><span data-stu-id="c0a5d-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="c0a5d-236">Puede utilizar el kit de herramientas de Azure para IntelliJ si quiere ejecutar aplicaciones Spark en Scala localmente en su estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="c0a5d-237">Normalmente las aplicaciones no necesitan tener acceso a los recursos de clúster, como el contenedor de almacenamiento, y se pueden ejecutar y probar de forma local.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="c0a5d-238">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="c0a5d-238">Prerequisite</span></span>
<span data-ttu-id="c0a5d-239">Mientras se ejecuta la aplicación Spark en Scala local en un equipo Windows, puede producirse una excepción, como se explica en [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="c0a5d-240">Esta excepción se produce porque falta WinUtils.exe en Windows.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="c0a5d-241">Para solucionar este error, [descargue el archivo ejecutable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) y guárdelo en una ubicación como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="c0a5d-242">Después, agregue una variable de entorno **HADOOP_HOME** y establezca el valor de la variable en **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="c0a5d-243">Ejecución de una aplicación Spark en Scala local</span><span class="sxs-lookup"><span data-stu-id="c0a5d-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="c0a5d-244">Inicie IntelliJ IDEA y cree un proyecto.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="c0a5d-245">En el cuadro de diálogo **Nuevo proyecto** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="c0a5d-246">a.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-246">a.</span></span> <span data-ttu-id="c0a5d-247">Seleccione **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Ejemplo de ejecución local de Spark en HDInsight [Scala]).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="c0a5d-248">b.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-248">b.</span></span> <span data-ttu-id="c0a5d-249">En la lista de **herramientas de compilación**, seleccione cualquiera de las siguientes, según sus necesidades:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="c0a5d-250">**Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="c0a5d-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="c0a5d-251">**SBT**, para administrar las dependencias y compilar el proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="c0a5d-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Cuadro de diálogo Nuevo proyecto](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="c0a5d-253">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="c0a5d-254">En la ventana que se muestra a continuación, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="c0a5d-255">a.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-255">a.</span></span> <span data-ttu-id="c0a5d-256">Escriba un nombre y una ubicación de proyecto.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-256">Enter a project name and location.</span></span>

    <span data-ttu-id="c0a5d-257">b.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-257">b.</span></span> <span data-ttu-id="c0a5d-258">En la lista desplegable **SDK de proyecto**, seleccione una versión de Java que sea posterior a la versión 1.7.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="c0a5d-259">c.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-259">c.</span></span> <span data-ttu-id="c0a5d-260">En la lista desplegable **Versión de Spark**, seleccione la versión de Scala que desea usar: Scala 2.11.x para Spark 2.0 o Scala 2.10.x para Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![Cuadro de diálogo Nuevo proyecto](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="c0a5d-262">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-262">Select **Finish**.</span></span>

6. <span data-ttu-id="c0a5d-263">La plantilla agrega un código de ejemplo (**LogQuery**) en la carpeta **src** que puede ejecutar localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Ubicación de LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="c0a5d-265">Haga clic con el botón derecho en la aplicación **LogQuery** y seleccione **Run "LogQuery"** (Ejecutar LogQuery).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="c0a5d-266">En la pestaña **Run** (Ejecutar) en la parte inferior verá una salida similar a la que se ve a continuación:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Resultado de la ejecución local de la aplicación Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="c0a5d-268">Conversión de las aplicaciones IntelliJ IDEA existentes para usar el kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c0a5d-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="c0a5d-269">Puede convertir las aplicaciones Spark en Scala existentes creadas en IntelliJ IDEA para que sean compatibles con el kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="c0a5d-270">Esto le permitirá utilizar el complemento para enviar las aplicaciones a un clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="c0a5d-271">Para una aplicación Spark en Scala existente creada con IntelliJ IDEA, abra el archivo .iml asociado.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="c0a5d-272">En el nivel raíz, hay un elemento de **module** similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="c0a5d-273">Edite el elemento para agregar `UniqueKey="HDInsightTool"` de forma que el elemento de **module** sea similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="c0a5d-274">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-274">Save the changes.</span></span> <span data-ttu-id="c0a5d-275">La aplicación ahora debe ser compatible con el kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="c0a5d-276">Puede comprobarlo si hace clic con el botón derecho en el nombre de proyecto en el explorador de proyectos.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="c0a5d-277">El menú emergente ahora debería tener la opción **Submit Spark Application to HDInsight** (Enviar aplicación Spark a HDInsight).</span><span class="sxs-lookup"><span data-stu-id="c0a5d-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c0a5d-278">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="c0a5d-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="c0a5d-279">Error en la ejecución local: *Please use a larger heap size* (Utilice un tamaño de montón mayor)</span><span class="sxs-lookup"><span data-stu-id="c0a5d-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="c0a5d-280">En Spark 1.6, si utiliza un SDK de Java de 32 bits durante la ejecución local, puede encontrar los siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="c0a5d-281">Estos errores se producen porque el tamaño del montón no es lo suficientemente grande como para que se ejecute Spark.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="c0a5d-282">Spark requiere al menos 471 MB.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="c0a5d-283">(para obtener más información, consulte [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081)). Una solución sencilla es utilizar un SDK de Java de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="c0a5d-284">También puede cambiar la configuración de JVM en IntelliJ agregando las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="c0a5d-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Incorporación de opciones a la casilla de opciones de máquina virtual en IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="c0a5d-286">P+F</span><span class="sxs-lookup"><span data-stu-id="c0a5d-286">FAQ</span></span>
<span data-ttu-id="c0a5d-287">Para enviar una aplicación a Azure Data Lake Store, elija el modo **Interactivo** durante el proceso de inicio de sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="c0a5d-288">Si selecciona el modo **Automatizado**, puede aparecer un error.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-288">If you select **Automated** mode, you can get an error.</span></span>

![inicio de sesión interactivo](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="c0a5d-290">Ahora se ha resuelto.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-290">Now, we resolved it.</span></span> <span data-ttu-id="c0a5d-291">Puede elegir un clúster de Azure Data Lake para enviar la aplicación con cualquier método de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="c0a5d-292">Comentarios y problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="c0a5d-292">Feedback and known issues</span></span>
<span data-ttu-id="c0a5d-293">Actualmente, la visualización de salidas de Spark directamente no se admite.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="c0a5d-294">Si tiene sugerencias o comentarios, o si se le presenta algún problema al usar este complemento, no dude en enviarnos un correo electrónico a la dirección hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c0a5d-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="c0a5d-295"><a name="seealso"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0a5d-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="c0a5d-296">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="c0a5d-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="c0a5d-297">Demostración</span><span class="sxs-lookup"><span data-stu-id="c0a5d-297">Demo</span></span>
* <span data-ttu-id="c0a5d-298">Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="c0a5d-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="c0a5d-299">Depuración remota (vídeo): [Uso del kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones Spark en clústeres de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="c0a5d-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="c0a5d-300">Escenarios</span><span class="sxs-lookup"><span data-stu-id="c0a5d-300">Scenarios</span></span>
* [<span data-ttu-id="c0a5d-301">Spark con BI: realización del análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="c0a5d-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c0a5d-302">Spark con Machine Learning: uso de Spark en HDInsight para analizar la temperatura de edificios con los datos del sistema de acondicionamiento de aire</span><span class="sxs-lookup"><span data-stu-id="c0a5d-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c0a5d-303">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="c0a5d-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c0a5d-304">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="c0a5d-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c0a5d-305">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0a5d-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="c0a5d-306">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c0a5d-306">Creating and running applications</span></span>
* [<span data-ttu-id="c0a5d-307">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="c0a5d-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c0a5d-308">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="c0a5d-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c0a5d-309">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="c0a5d-309">Tools and extensions</span></span>
* [<span data-ttu-id="c0a5d-310">Uso del kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones Spark mediante VPN</span><span class="sxs-lookup"><span data-stu-id="c0a5d-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c0a5d-311">Uso del kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones Spark mediante SSH</span><span class="sxs-lookup"><span data-stu-id="c0a5d-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="c0a5d-312">Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="c0a5d-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="c0a5d-313">Uso de las herramientas de HDInsight del kit de herramientas de Azure para Eclipse con el fin de crear aplicaciones Spark</span><span class="sxs-lookup"><span data-stu-id="c0a5d-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="c0a5d-314">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0a5d-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c0a5d-315">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0a5d-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c0a5d-316">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="c0a5d-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c0a5d-317">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="c0a5d-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="c0a5d-318">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="c0a5d-318">Managing resources</span></span>
* [<span data-ttu-id="c0a5d-319">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="c0a5d-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c0a5d-320">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="c0a5d-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

