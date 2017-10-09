---
title: Kit de herramientas de Azure para IntelliJ con espacio aislado de Hortonworks aaaUse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse herramientas de HDInsight en el Kit de herramientas de Azure para IntelliJ con Hortonworks Sandbox."
keywords: herramientas de hadoop,consulte de hive,intellij,hortonworks sandbox,kit de herramientas de azure para intellij
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="fd778-104">Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="fd778-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="fd778-105">Obtenga información acerca de cómo toouse HDInsight Tools para aplicaciones de Apache Scala toodevelop IntelliJ y, a continuación, probar Hola aplicaciones en [espacio aislado de Hortonworks](http://hortonworks.com/products/sandbox/) ejecutando en la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fd778-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="fd778-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) es un entorno de desarrollo integrado (IDE) de Java para el desarrollo de software informático.</span><span class="sxs-lookup"><span data-stu-id="fd778-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="fd778-107">Después de que haya desarrollado y probado las aplicaciones en el espacio aislado de Hortonworks, puede moverlos demasiado[HDInsight de Azure](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fd778-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd778-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd778-108">Prerequisites</span></span>

<span data-ttu-id="fd778-109">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd778-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="fd778-110">Hortonworks Data Platform (HDP) 2.4 en Hortonworks Sandbox ejecutándose en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="fd778-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="fd778-111">tooconfigure HDP, consulte [empezar a trabajar en el ecosistema de Hadoop de hello con un espacio aislado de Hadoop en una máquina virtual](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd778-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="fd778-112">Las herramientas de HDInsight para IntelliJ solo se han probado con HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="fd778-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="fd778-113">Expanda tooget HDP 2.4, **Archive de espacio aislado de Hortonworks** en hello [sitio de descargas de espacio aislado de Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="fd778-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="fd778-114">[Kit de desarrolladores de Java (JDK) versión 1.8 o posterior](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="fd778-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="fd778-115">Hola Kit de herramientas de Azure requiere JDK para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="fd778-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="fd778-116">[Edición de la Comunidad de IDEA IntelliJ](https://www.jetbrains.com/idea/download) con hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) complemento hello y [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) complemento.</span><span class="sxs-lookup"><span data-stu-id="fd778-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="fd778-117">Herramientas de HDInsight para IntelliJ está disponible como parte del Kit de herramientas de Azure para IntelliJ Hola.</span><span class="sxs-lookup"><span data-stu-id="fd778-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="fd778-118">tooinstall Hola complementos, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd778-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="fd778-119">Abra IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="fd778-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="fd778-120">En hello **bienvenida** pantalla, seleccione **configurar**y, a continuación, seleccione **complementos**.</span><span class="sxs-lookup"><span data-stu-id="fd778-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="fd778-121">Seleccione **JetBrains instalar complemento** en la esquina inferior izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd778-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="fd778-122">Usar hello toosearch de función de búsqueda para **Scala**y, a continuación, seleccione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="fd778-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="fd778-123">Seleccione **reiniciar IntelliJ IDEA** instalación de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fd778-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="fd778-124">Hola de Repita el paso 4 y 5 tooinstall **Azure Toolkit for IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="fd778-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="fd778-125">Para obtener más información, consulte [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="fd778-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="fd778-126">Creación de una aplicación de Scala en Spark</span><span class="sxs-lookup"><span data-stu-id="fd778-126">Create a Spark Scala application</span></span>

<span data-ttu-id="fd778-127">En esta sección, creará un proyecto de Scala de ejemplo con IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="fd778-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="fd778-128">En la siguiente sección hello, vincular IDEA IntelliJ toohello Hortonworks espacio aislado (emulador) antes de enviar proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="fd778-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="fd778-129">Abra IntelliJ IDEA desde la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fd778-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="fd778-130">Hola **nuevo proyecto** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd778-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="fd778-131">a.</span><span class="sxs-lookup"><span data-stu-id="fd778-131">a.</span></span> <span data-ttu-id="fd778-132">Seleccione **HDInsight** > **Spark en HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="fd778-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="fd778-133">b.</span><span class="sxs-lookup"><span data-stu-id="fd778-133">b.</span></span> <span data-ttu-id="fd778-134">Hola **herramienta de compilación** , seleccione cualquiera de hello siguientes, según la necesidad de tooyour:</span><span class="sxs-lookup"><span data-stu-id="fd778-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="fd778-135">**Maven**, para la compatibilidad con el asistente para crear un proyecto de Scala</span><span class="sxs-lookup"><span data-stu-id="fd778-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="fd778-136">**SBT**, para administrar las dependencias de Hola y compilar para el proyecto de Scala Hola</span><span class="sxs-lookup"><span data-stu-id="fd778-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![cuadro de diálogo nuevo proyecto de Hola](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="fd778-138">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="fd778-138">Select **Next**.</span></span>

3. <span data-ttu-id="fd778-139">Hola siguiente **nuevo proyecto** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd778-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![Creación de las propiedades del proyecto de Scala en IntelliJ](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="fd778-141">a.</span><span class="sxs-lookup"><span data-stu-id="fd778-141">a.</span></span> <span data-ttu-id="fd778-142">Hola **nombre del proyecto** cuadro, escriba un nombre de proyecto.</span><span class="sxs-lookup"><span data-stu-id="fd778-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="fd778-143">b.</span><span class="sxs-lookup"><span data-stu-id="fd778-143">b.</span></span> <span data-ttu-id="fd778-144">Hola **ubicación del proyecto** cuadro, escriba una ubicación de proyecto.</span><span class="sxs-lookup"><span data-stu-id="fd778-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="fd778-145">c.</span><span class="sxs-lookup"><span data-stu-id="fd778-145">c.</span></span> <span data-ttu-id="fd778-146">Siguiente toohello **proyecto SDK** lista desplegable, seleccione **New**, seleccione **JDK**, y, a continuación, especifique la carpeta Hola de Java JDK versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="fd778-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="fd778-147">Seleccione **Java 1.8** para clúster de hello Spark 2.x, o bien seleccione **Java 1.7** para clúster de hello Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="fd778-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="fd778-148">ubicación predeterminada de Hello es C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="fd778-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="fd778-149">d.</span><span class="sxs-lookup"><span data-stu-id="fd778-149">d.</span></span> <span data-ttu-id="fd778-150">Hola **versión Spark** lista desplegable, el Asistente para crear un proyecto Scala integra con la versión adecuada de Hola de SDK de Spark y Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="fd778-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="fd778-151">Si la versión de clúster de Spark hello es anterior a la 2.0, seleccione **inspirará 1.x**.</span><span class="sxs-lookup"><span data-stu-id="fd778-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="fd778-152">De lo contrario, seleccione **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="fd778-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="fd778-153">Este ejemplo utiliza Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="fd778-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="fd778-154">Asegúrese de que está usando repositorio Hola marcado Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="fd778-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="fd778-155">No utilice repositorio Hola marcado Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="fd778-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="fd778-156">Seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="fd778-156">Select **Finish**.</span></span>

5. <span data-ttu-id="fd778-157">Si hello **proyecto** vista ya no está abierta, presione **Alt + 1** tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="fd778-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="fd778-158">En **el Explorador de proyectos**, expanda el proyecto de hello y, a continuación, seleccione **src**.</span><span class="sxs-lookup"><span data-stu-id="fd778-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="fd778-159">Haga clic en **src**, seleccione demasiado**New**y, a continuación, seleccione **Scala clase**.</span><span class="sxs-lookup"><span data-stu-id="fd778-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="fd778-160">Hola **nombre** cuadro, escriba un nombre en hello **tipo** cuadro, seleccione **objeto**y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fd778-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![ventana de crear una nueva clase de Scala Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="fd778-162">En archivo de .scala de hello, pegue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="fd778-162">In hello .scala file, paste hello following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="fd778-163">En hello **generar** menú, seleccione **proyecto de compilación**.</span><span class="sxs-lookup"><span data-stu-id="fd778-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="fd778-164">Asegúrese de que la compilación de Hola se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="fd778-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="fd778-165">Vincular toohello espacio aislado de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="fd778-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="fd778-166">Antes de poder enlazar tooa Hortonworks espacio aislado (emulador), debe tener una aplicación de IntelliJ existente.</span><span class="sxs-lookup"><span data-stu-id="fd778-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="fd778-167">emulador de tooan toolink, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd778-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="fd778-168">Proyecto abierto hello en IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="fd778-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="fd778-169">En hello **vista** menú, seleccione **herramientas de Windows**y, a continuación, seleccione **explorador Azure**.</span><span class="sxs-lookup"><span data-stu-id="fd778-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="fd778-170">Expanda **Azure**, haga clic con el botón derecho en **HDInsight** y luego seleccione **Link an Emulator** (Vincular un emulador).</span><span class="sxs-lookup"><span data-stu-id="fd778-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="fd778-171">Hola **vínculo A nuevo emulador** ventana, escriba la contraseña de Hola que ha configurado para la cuenta raíz de Hola de hello espacio aislado de Hortonworks, escriba toothose similar de valores en la siguiente captura de pantalla de hello y, a continuación, seleccione **Aceptar** .</span><span class="sxs-lookup"><span data-stu-id="fd778-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![ventana de "Vínculo a nuevo emulador" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="fd778-173">emulador de hello tooconfigure, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="fd778-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="fd778-174">Al emulador Hola está conectado correctamente, emulador hello (Hortonworks espacio aislado) se muestra en el nodo de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd778-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="fd778-175">Enviar Hola Spark Scala aplicación toohello espacio aislado de Hortonworks</span><span class="sxs-lookup"><span data-stu-id="fd778-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="fd778-176">Después de haber vinculado emulador de toohello IntelliJ IDEA, puede enviar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="fd778-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="fd778-177">Hola toosubmit un emulador tooan del proyecto, después de:</span><span class="sxs-lookup"><span data-stu-id="fd778-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="fd778-178">En **el Explorador de proyectos**, haga clic en proyecto de hello y, a continuación, seleccione **enviar Spark aplicación tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fd778-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="fd778-179">Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd778-179">Do hello following:</span></span>

    <span data-ttu-id="fd778-180">a.</span><span class="sxs-lookup"><span data-stu-id="fd778-180">a.</span></span> <span data-ttu-id="fd778-181">Hola **clúster Spark (solamente para Linux)** lista desplegable, seleccione el espacio aislado de Hortonworks local.</span><span class="sxs-lookup"><span data-stu-id="fd778-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="fd778-182">b.</span><span class="sxs-lookup"><span data-stu-id="fd778-182">b.</span></span> <span data-ttu-id="fd778-183">Hola **nombre de la clase principal** cuadro, elija o escriba el nombre de la clase principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd778-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="fd778-184">Para este tutorial, se denomina hello **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="fd778-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="fd778-185">Seleccione **Submit** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="fd778-185">Select **Submit**.</span></span> <span data-ttu-id="fd778-186">los registros de envío de trabajos de Hola se muestran en la ventana de herramienta de envío de hello Spark.</span><span class="sxs-lookup"><span data-stu-id="fd778-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd778-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd778-187">Next steps</span></span>

- <span data-ttu-id="fd778-188">toolearn cómo ir demasiado toocreate aplicaciones de Spark para HDInsight mediante las herramientas de HDInsight para IntelliJ,[Use herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de clúster de HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="fd778-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="fd778-189">toowatch un vídeo de herramientas de HDInsight para IntelliJ, vaya demasiado[introducir herramientas de HDInsight para IntelliJ para el desarrollo de Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="fd778-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="fd778-190">toolearn cómo las aplicaciones de Spark toodebug mediante Hola Kit de herramientas de forma remota en HDInsight a través de SSH, vaya demasiado[depurar de forma remota aplicaciones Spark en un clúster de HDInsight con el Kit de herramientas de Azure para IntelliJ a través de SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="fd778-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="fd778-191">toolearn cómo las aplicaciones de Spark toodebug mediante Hola Kit de herramientas de forma remota en HDInsight a través de VPN, vaya demasiado[Use herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toodebug Spark para aplicaciones de forma remota en el clúster de HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="fd778-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="fd778-192">toolearn cómo toouse herramientas de HDInsight para Eclipse toocreate una aplicación Spark, vaya demasiado[Use herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="fd778-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="fd778-193">toowatch un vídeo de herramientas de HDInsight para Eclipse, vaya demasiado[usar la herramienta de HDInsight para aplicaciones de Eclipse toocreate Spark](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="fd778-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
