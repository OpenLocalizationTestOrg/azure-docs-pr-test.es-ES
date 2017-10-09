---
title: "aaaCreate Scala aplicación toorun en clústeres de Spark - HDInsight de Azure | Documentos de Microsoft"
description: "Crear una aplicación de Spark escrita en Scala con Apache Maven como Hola de compilación del sistema y Arquetipo Maven existente para Scala proporcionada por IntelliJ IDEA."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="4f47b-103">Crear un toorun de aplicación Scala Maven en clúster de Apache Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f47b-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="4f47b-104">Obtenga información acerca de cómo toocreate una aplicación de Spark escrita en Scala con Maven IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="4f47b-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="4f47b-105">artículo Hello usa a Apache Maven cuando Hola sistema de compilación y se inicia con Arquetipo Maven existente por Scala proporcionada por IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="4f47b-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="4f47b-106">Crear una aplicación Scala en IntelliJ IDEA implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4f47b-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="4f47b-107">Use Maven como sistema de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="4f47b-108">Actualizar las dependencias del módulo modelo de objeto de proyecto (POM) archivo tooresolve Spark.</span><span class="sxs-lookup"><span data-stu-id="4f47b-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="4f47b-109">Escriba la aplicación con Scala.</span><span class="sxs-lookup"><span data-stu-id="4f47b-109">Write your application in Scala.</span></span>
* <span data-ttu-id="4f47b-110">Generar un archivo jar que puede ser enviado tooHDInsight Spark clústeres.</span><span class="sxs-lookup"><span data-stu-id="4f47b-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="4f47b-111">Ejecute la aplicación hello en un clúster de Spark mediante Livio.</span><span class="sxs-lookup"><span data-stu-id="4f47b-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="4f47b-112">HDInsight también proporciona un proceso de hello IntelliJ IDEA tooease de herramienta de complemento de crear y enviar aplicaciones tooan clúster de HDInsight Spark en Linux.</span><span class="sxs-lookup"><span data-stu-id="4f47b-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="4f47b-113">Para obtener más información, consulte [complemento de herramientas de HDInsight de uso para toocreate IntelliJ IDEA y enviar solicitudes de Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="4f47b-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4f47b-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4f47b-114">Prerequisites</span></span>

* <span data-ttu-id="4f47b-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f47b-115">An Azure subscription.</span></span> <span data-ttu-id="4f47b-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4f47b-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="4f47b-117">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f47b-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="4f47b-118">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4f47b-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="4f47b-119">Kit de desarrollo de Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="4f47b-119">Oracle Java Development kit.</span></span> <span data-ttu-id="4f47b-120">Se puede instalar desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="4f47b-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="4f47b-121">Un IDE de Java.</span><span class="sxs-lookup"><span data-stu-id="4f47b-121">A Java IDE.</span></span> <span data-ttu-id="4f47b-122">En este artículo se usa IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="4f47b-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="4f47b-123">Se puede instalar desde [aquí](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="4f47b-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="4f47b-124">Instale el complemento de Scala para IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="4f47b-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="4f47b-125">Si no una petición no instalación IntelliJ IDEA para habilitar el complemento Scala, inicie IntelliJ IDEA y vaya a través de hello siguiendo los pasos tooinstall Hola complemento:</span><span class="sxs-lookup"><span data-stu-id="4f47b-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="4f47b-126">Inicie IntelliJ IDEA y, en la pantalla de bienvenida, haga clic en **Configure** (Configurar) y luego en **Plugins** (Complementos).</span><span class="sxs-lookup"><span data-stu-id="4f47b-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Habilitar complemento de Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="4f47b-128">En la siguiente pantalla de bienvenida, haga clic en **JetBrains instalar complemento** desde la esquina inferior izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="4f47b-129">Hola **examinar JetBrains complementos** cuadro de diálogo que se abre, busque Scala y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Instalar complemento de Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="4f47b-131">Después de hello complemento se instala correctamente, haga clic en hello **botón de reiniciar la IDEA de IntelliJ** toorestart Hola IDE.</span><span class="sxs-lookup"><span data-stu-id="4f47b-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="4f47b-132">Creación de un proyecto de Scala independiente</span><span class="sxs-lookup"><span data-stu-id="4f47b-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="4f47b-133">Inicie IntelliJ IDEA y cree un nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="4f47b-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="4f47b-134">En el cuadro de diálogo de proyecto nuevo hello, asegúrese de Hola siguientes opciones y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Crear proyecto de Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="4f47b-136">Seleccione **Maven** como tipo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="4f47b-137">Especifique un **SDK de proyecto**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="4f47b-138">Haga clic en nuevo y navegue toohello directorio de instalación de Java, normalmente `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="4f47b-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="4f47b-139">Seleccione hello **crear desde Arquetipo** opción.</span><span class="sxs-lookup"><span data-stu-id="4f47b-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="4f47b-140">Seleccionar en lista Hola de archetypes **org.scala tools.archetypes:scala Arquetipo simple**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="4f47b-141">Esto creará estructura de directorio de Hola y descargar Hola necesario predeterminado dependencias toowrite Scala programa.</span><span class="sxs-lookup"><span data-stu-id="4f47b-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="4f47b-142">Proporcione los valores correspondientes para **GroupId**, **ArtifactId** y **Version**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="4f47b-143">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-143">Click **Next**.</span></span>
3. <span data-ttu-id="4f47b-144">En el siguiente cuadro de diálogo hello, donde puede especificar el directorio particular de Maven y otras opciones de usuario, acepte los valores predeterminados de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="4f47b-145">En el último cuadro de diálogo hello, especifique un nombre de proyecto y una ubicación y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="4f47b-146">Eliminar hello **MySpec.Scala** de archivos en **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="4f47b-147">No es necesario para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4f47b-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="4f47b-148">Si es necesario, cambie el nombre de archivos de origen y de prueba de hello predeterminados.</span><span class="sxs-lookup"><span data-stu-id="4f47b-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="4f47b-149">Desde el panel izquierdo de Hola Hola IntelliJ IDEA, navegue demasiado**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="4f47b-150">Haga clic en **App.scala**, haga clic en **refactorizar**, haga clic en cambiar el nombre archivo y en el cuadro de diálogo de hello, especifique el nuevo nombre de hello para la aplicación hello y, a continuación, haga clic en **refactorizar**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![Cambiar el nombre de los archivos](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="4f47b-152">En pasos posteriores de hello, actualizará hello pom.xml toodefine Hola dependencias Hola Spark Scala aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f47b-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="4f47b-153">Para esas dependencias toobe descarga y resuelve automáticamente, que debe configurar a Maven en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="4f47b-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Configurar Maven para descargas automáticas](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="4f47b-155">De hello **archivo** menú, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="4f47b-156">Hola **configuración** diálogo cuadro, vaya demasiado**de compilación, ejecución, implementación** > **herramientas de generación de** > **Maven**  >  **Importar**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="4f47b-157">Seleccione la opción de hello demasiado**Maven importar proyectos automáticamente**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="4f47b-158">Haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="4f47b-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="4f47b-159">Actualizar tooinclude del archivo de origen de hello Scala el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f47b-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="4f47b-160">Abra y reemplace Hola existente código de ejemplo con el siguiente código de hello y guardar los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="4f47b-161">Este código lee los datos de Hola de hello HVAC.csv (disponible en todos los clústeres de HDInsight Spark), se recuperan las filas de Hola que sólo tienen un dígito en la sexta columna de Hola y escribe la salida de hello demasiado**/HVACOut** en almacenamiento de saludo predeterminado contenedor para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="4f47b-162">Actualizar pom.xml Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="4f47b-163">En `<project>\<properties>` agregue Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="4f47b-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="4f47b-164">En `<project>\<dependencies>` agregue Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="4f47b-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="4f47b-165">Guardar cambios toopom.xml.</span><span class="sxs-lookup"><span data-stu-id="4f47b-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="4f47b-166">Crear el archivo .jar Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-166">Create hello .jar file.</span></span> <span data-ttu-id="4f47b-167">IntelliJ IDEA permite crear JAR como un artefacto de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="4f47b-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="4f47b-168">Realizar pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="4f47b-169">De hello **archivo** menú, haga clic en **estructura del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="4f47b-170">Hola **estructura del proyecto** cuadro de diálogo, haga clic en **artefactos** y, a continuación, haga clic en hello además de símbolos.</span><span class="sxs-lookup"><span data-stu-id="4f47b-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="4f47b-171">En el cuadro de diálogo emergente de hello, haga clic en **JAR**y, a continuación, haga clic en **de módulos con dependencias**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="4f47b-173">Hola **crear JAR de módulos** diálogo cuadro, haga clic en el botón de puntos suspensivos hello (![puntos suspensivos](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) contra Hola **clase principal**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="4f47b-174">Hola **seleccionar clase de Main** cuadro de diálogo, clase de hello seleccione aparece de forma predeterminada y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="4f47b-176">Hola **crear JAR de módulos** diálogo cuadro, asegúrese de que esa opción Hola demasiado**extraer toohello destino JAR** está seleccionada y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="4f47b-177">Así se crea un archivo JAR único con todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="4f47b-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="4f47b-179">pestaña de diseño de salida de Hello enumera todos los archivos JAR Hola que se incluyen como parte del proyecto de Maven Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="4f47b-180">Puede seleccionar y Hola delete aquellos en los que Hola Scala aplicación no tiene ninguna dependencia directa.</span><span class="sxs-lookup"><span data-stu-id="4f47b-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="4f47b-181">Para la aplicación hello vamos a crear a continuación, puede quitar todos menos Hola último (**salida de compilación SparkSimpleApp**).</span><span class="sxs-lookup"><span data-stu-id="4f47b-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="4f47b-182">Seleccione toodelete de archivos JAR de hello y, a continuación, haga clic en hello **eliminar** icono.</span><span class="sxs-lookup"><span data-stu-id="4f47b-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="4f47b-184">Asegúrese de que **compilar en hacer** casilla está activada, lo que garantiza que jar Hola se crea cada vez proyecto Hola se compila o se actualiza.</span><span class="sxs-lookup"><span data-stu-id="4f47b-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="4f47b-185">Haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="4f47b-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="4f47b-186">En la barra de menús de hello, haga clic en **generar**y, a continuación, haga clic en **proyecto realizar**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="4f47b-187">También puede hacer clic en **Generar artefactos** jar de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4f47b-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="4f47b-188">jar de salida Hello se crea una en **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="4f47b-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![Crear archivo JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="4f47b-190">Ejecutar la aplicación hello en clúster de Spark Hola</span><span class="sxs-lookup"><span data-stu-id="4f47b-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="4f47b-191">aplicación de hello toorun en clúster de hello, debe hacer los siguiente Hola:</span><span class="sxs-lookup"><span data-stu-id="4f47b-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="4f47b-192">**Blob de almacenamiento de Azure de copia Hola aplicación jar toohello** asociado con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f47b-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="4f47b-193">Puede usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), por lo que utilidad, toodo un comando de línea.</span><span class="sxs-lookup"><span data-stu-id="4f47b-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="4f47b-194">Hay muchos otros clientes, así que puede utilizar datos de tooupload.</span><span class="sxs-lookup"><span data-stu-id="4f47b-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="4f47b-195">Puede encontrar más información al respecto en [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="4f47b-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="4f47b-196">**Usar Livio toosubmit un trabajo de la aplicación de forma remota** toohello clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="4f47b-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="4f47b-197">Clústeres de Spark en HDInsight incluye Livio que expone REST extremos tooremotely enviar trabajos de Spark.</span><span class="sxs-lookup"><span data-stu-id="4f47b-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="4f47b-198">Para obtener más información, vea [Envío remoto de trabajos de Spark mediante la utilización de Livy con clústeres Spark en HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="4f47b-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="4f47b-199">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="4f47b-199">Next step</span></span>

<span data-ttu-id="4f47b-200">En este artículo se habrá aprendido cómo toocreate una aplicación de scala Spark.</span><span class="sxs-lookup"><span data-stu-id="4f47b-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="4f47b-201">Avance toohello siguiente artículo toolearn cómo toorun esta aplicación en un HDInsight Spark de clúster mediante Livio.</span><span class="sxs-lookup"><span data-stu-id="4f47b-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="4f47b-202">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="4f47b-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

