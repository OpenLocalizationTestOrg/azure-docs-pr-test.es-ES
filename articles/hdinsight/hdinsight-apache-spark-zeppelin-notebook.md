---
title: "clúster de blocs de notas de aaaUse Zeppeling con Apache Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Instrucciones paso a paso sobre cómo se agrupa los blocs de notas de toouse Zeppeling con Apache Spark en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="e73ed-103">Uso de cuadernos de Zeppelin con un clúster Apache Spark en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e73ed-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="e73ed-104">Clústeres de HDInsight Spark incluyen blocs de notas de Zeppeling que puede usar los trabajos de Spark toorun.</span><span class="sxs-lookup"><span data-stu-id="e73ed-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="e73ed-105">En este artículo, aprenderá cómo toouse Hola Bloc de notas de Zeppeling en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e73ed-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e73ed-106">Los notebooks de Zeppelin están disponibles solo para Spark 1.6.3 en HDInsight 3.5 y Spark 2.1.0 en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e73ed-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="e73ed-107">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="e73ed-107">**Prerequisites:**</span></span>

* <span data-ttu-id="e73ed-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e73ed-108">An Azure subscription.</span></span> <span data-ttu-id="e73ed-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e73ed-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e73ed-110">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e73ed-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e73ed-111">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e73ed-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="e73ed-112">Inicio de un cuaderno de Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="e73ed-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="e73ed-113">En la hoja de clúster de Spark hello, haga clic en **panel clúster**y, a continuación, haga clic en **Bloc de notas de Zeppeling**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="e73ed-114">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e73ed-115">También puede tener acceso a hello Zeppeling Bloc de notas para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="e73ed-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="e73ed-116">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="e73ed-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="e73ed-117">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="e73ed-117">Create a new notebook.</span></span> <span data-ttu-id="e73ed-118">En el panel de encabezado de hello, haga clic en **Bloc de notas**y, a continuación, haga clic en **crear nueva nota**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="e73ed-119">![Creación de un nuevo cuaderno de Zeppeling](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Creación de un nuevo cuaderno de Zeppeling")</span><span class="sxs-lookup"><span data-stu-id="e73ed-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="e73ed-120">Escriba un nombre para el Bloc de notas de hello y, a continuación, haga clic en **crear nota**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="e73ed-121">Asegúrese también de que el encabezado de Bloc de notas de hello muestra un estado conectado.</span><span class="sxs-lookup"><span data-stu-id="e73ed-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="e73ed-122">Se indica mediante un punto verde en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="e73ed-123">![Estado del cuaderno de Zeppeling](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Estado del cuaderno de Zeppeling")</span><span class="sxs-lookup"><span data-stu-id="e73ed-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="e73ed-124">Cargue los datos de ejemplo en una tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="e73ed-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="e73ed-125">Cuando se crea un clúster de Spark en HDInsight, archivo de datos de ejemplo de Hola, **hvac.csv**, es copiada toohello asociado de cuenta de almacenamiento en **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="e73ed-126">En que se crea de forma predeterminada en Bloc de notas nuevo Hola párrafo vacío de hello, pegue Hola siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="e73ed-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="e73ed-127">Presione **MAYÚS + ENTRAR** o haga clic en hello **reproducir** botón para el fragmento de código de hello párrafo toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="e73ed-128">estado de Hello en la esquina derecha de Hola de párrafo Hola debe avanzan desde que se esté listo, pendiente, tooFINISHED de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e73ed-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="e73ed-129">salida de Hello aparezca en parte inferior de Hola de hello mismo párrafo.</span><span class="sxs-lookup"><span data-stu-id="e73ed-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="e73ed-130">captura de pantalla de Hello es similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e73ed-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="e73ed-131">![Creación de una tabla temporal a partir de datos sin procesar](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Creación de una tabla temporal a partir de datos sin procesar")</span><span class="sxs-lookup"><span data-stu-id="e73ed-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="e73ed-132">También puede proporcionar un párrafo de tooeach de título.</span><span class="sxs-lookup"><span data-stu-id="e73ed-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="e73ed-133">En la esquina derecha de hello, haga clic en hello **configuración** icono y, a continuación, haga clic en **Mostrar título**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="e73ed-134">Ahora puede ejecutar instrucciones SQL de Spark en hello **hvac** tabla.</span><span class="sxs-lookup"><span data-stu-id="e73ed-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="e73ed-135">Pegue Hola después de consulta en un párrafo nuevo.</span><span class="sxs-lookup"><span data-stu-id="e73ed-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="e73ed-136">consulta de Hello recupera el identificador de edificio de Hola y diferenciar hello en destino hello y temperaturas reales de cada edificio, en una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="e73ed-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="e73ed-137">Presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="e73ed-138">Hola **% sql** instrucción al principio de hello indica Livio Scala intérprete de hello Bloc de notas toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="e73ed-139">Hello captura de pantalla siguiente muestra el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="e73ed-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="e73ed-140">![Ejecutar una instrucción de Spark SQL mediante el Bloc de notas de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "ejecutar una instrucción de Spark SQL mediante el Bloc de notas de Hola")</span><span class="sxs-lookup"><span data-stu-id="e73ed-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="e73ed-141">Haga clic en hello Mostrar opciones (resaltado en el rectángulo) tooswitch entre diferentes representaciones de hello mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="e73ed-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="e73ed-142">Haga clic en **configuración** toochoose qué constituye Hola clave y valores de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="e73ed-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="e73ed-143">Hola captura de pantalla anterior se usa **buildingID** como clave de Hola y promedio de Hola de **temp_diff** como valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="e73ed-144">También puede ejecutar instrucciones SQL de Spark mediante variables de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="e73ed-145">Hola fragmento de código siguiente se muestra cómo toodefine una variable, **Temp**, en la consulta de hello cuyos valores posibles son Hola desea tooquery con.</span><span class="sxs-lookup"><span data-stu-id="e73ed-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="e73ed-146">Cuando ejecuta consultas de Hola por primera vez, una lista desplegable se rellena automáticamente con valores de hello especificados para la variable de saludo.</span><span class="sxs-lookup"><span data-stu-id="e73ed-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="e73ed-147">Pegue este fragmento de código en un nuevo párrafo y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="e73ed-148">Hello captura de pantalla siguiente muestra el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="e73ed-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="e73ed-149">![Ejecutar una instrucción de Spark SQL mediante el Bloc de notas de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "ejecutar una instrucción de Spark SQL mediante el Bloc de notas de Hola")</span><span class="sxs-lookup"><span data-stu-id="e73ed-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="e73ed-150">Para las consultas posteriores, puede seleccionar un nuevo valor de lista desplegable de Hola y vuelva a ejecutar consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="e73ed-151">Haga clic en **configuración** toochoose qué constituye Hola clave y valores de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="e73ed-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="e73ed-152">Hola captura de pantalla anterior se usa **buildingID** como clave de hello, Hola promedio de **temp_diff** como valor de hello, y **targettemp** como grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="e73ed-153">Reinicie la aplicación hello de Livio intérprete tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="e73ed-154">toodo, abra Configuración de intérprete haciendo clic en hello registra en nombre de usuario desde la esquina superior derecha de hello y, a continuación, haga clic en **intérprete**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="e73ed-155">![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")</span><span class="sxs-lookup"><span data-stu-id="e73ed-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="e73ed-156">Desplácese tooLivy configuración de intérprete y, a continuación, haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="e73ed-157">![Reinicie Hola Livio intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar hello Zeppeling intepreter")</span><span class="sxs-lookup"><span data-stu-id="e73ed-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="e73ed-158">¿Cómo se puede usar los paquetes externos con el Bloc de notas de Hola?</span><span class="sxs-lookup"><span data-stu-id="e73ed-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="e73ed-159">Puede configurar el Bloc de notas de hello Zeppeling en clústeres de Apache Spark en HDInsight (Linux) toouse externos, contribuyeron a la Comunidad de paquetes que no se incluye fuera-de-predeterminada en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="e73ed-160">Puede buscar hello [repositorio Maven](http://search.maven.org/) para la lista completa de Hola de paquetes que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="e73ed-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="e73ed-161">También puede obtener una lista de paquetes disponibles de otras fuentes.</span><span class="sxs-lookup"><span data-stu-id="e73ed-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="e73ed-162">Por ejemplo, dispone de la lista completa de los paquetes externos aportados por la comunidad en [Spark Packages](http://spark-packages.org/)(Paquetes Spark).</span><span class="sxs-lookup"><span data-stu-id="e73ed-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="e73ed-163">En este artículo, verá cómo hello toouse [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paquete con el Bloc de notas de hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e73ed-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="e73ed-164">Abra la configuración del intérprete.</span><span class="sxs-lookup"><span data-stu-id="e73ed-164">Open interpreter settings.</span></span> <span data-ttu-id="e73ed-165">Desde la esquina superior derecha de hello, haga clic en hello registrado en nombre de usuario y, a continuación, haga clic en **intérprete**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="e73ed-166">![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")</span><span class="sxs-lookup"><span data-stu-id="e73ed-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="e73ed-167">Desplácese tooLivy configuración de intérprete y, a continuación, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="e73ed-168">![Cambio de la configuración del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Cambio de la configuración del intérprete")</span><span class="sxs-lookup"><span data-stu-id="e73ed-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="e73ed-169">Agregue una nueva clave denominada **livy.spark.jars.packages** y establezca su valor en formato de hello `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="e73ed-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="e73ed-170">Por lo tanto, si desea hello toouse [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paquete, debe establecer valor de Hola de clave de hello demasiado`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="e73ed-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="e73ed-171">![Cambio de la configuración del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Cambio de la configuración del intérprete")</span><span class="sxs-lookup"><span data-stu-id="e73ed-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="e73ed-172">Haga clic en **guardar** y, a continuación, reinicie Hola intérprete Livio.</span><span class="sxs-lookup"><span data-stu-id="e73ed-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="e73ed-173">**Sugerencia**: si desea que toounderstand forma de especificar tooarrive como valor de Hola de clave de hello anteriormente, a continuación cómo.</span><span class="sxs-lookup"><span data-stu-id="e73ed-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="e73ed-174">a.</span><span class="sxs-lookup"><span data-stu-id="e73ed-174">a.</span></span> <span data-ttu-id="e73ed-175">Busque el paquete de Hola Hola Maven repositorio.</span><span class="sxs-lookup"><span data-stu-id="e73ed-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="e73ed-176">En este tutorial, hemos utilizado [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="e73ed-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="e73ed-177">b.</span><span class="sxs-lookup"><span data-stu-id="e73ed-177">b.</span></span> <span data-ttu-id="e73ed-178">Repositorio de hello, recopilar los valores de hello de **GroupId**, **ArtifactId**, y **versión**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="e73ed-179">![Uso de paquetes externos con cuadernos de Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Uso de paquetes externos con cuadernos de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="e73ed-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="e73ed-180">c.</span><span class="sxs-lookup"><span data-stu-id="e73ed-180">c.</span></span> <span data-ttu-id="e73ed-181">Concatenar valores de hello tres, separados por dos puntos (**:**).</span><span class="sxs-lookup"><span data-stu-id="e73ed-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="e73ed-182">¿Dónde está Hola blocs de notas Zeppeling guardados?</span><span class="sxs-lookup"><span data-stu-id="e73ed-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="e73ed-183">blocs de notas de Hello Zeppeling se guardan toohello headnodes de clúster.</span><span class="sxs-lookup"><span data-stu-id="e73ed-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="e73ed-184">Por lo tanto, si elimina el clúster de hello, blocs de notas de Hola se eliminarán también.</span><span class="sxs-lookup"><span data-stu-id="e73ed-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="e73ed-185">Si desea toopreserve los blocs de notas para su uso posterior en otros clústeres, debe exportar cuando haya terminado de ejecutar trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="e73ed-186">tooexport un bloc de notas, haga clic en hello **exportar** icono tal y como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="e73ed-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="e73ed-187">![Descargar el Bloc de notas](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Bloc de notas de Hola de descarga")</span><span class="sxs-lookup"><span data-stu-id="e73ed-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="e73ed-188">Esto ahorra Bloc de notas de Hola como un archivo JSON en la ubicación de descarga.</span><span class="sxs-lookup"><span data-stu-id="e73ed-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="e73ed-189">Administración de sesiones de Livy</span><span class="sxs-lookup"><span data-stu-id="e73ed-189">Livy session management</span></span>
<span data-ttu-id="e73ed-190">Cuando se ejecuta el primer párrafo de código de hello en el Bloc de notas Zeppeling, se crea una nueva sesión Livio en el clúster de HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e73ed-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="e73ed-191">Esta sesión se compartirá con todos los cuadernos de Zeppelin Notebook que cree en el futuro.</span><span class="sxs-lookup"><span data-stu-id="e73ed-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="e73ed-192">If para algunos hello motivo Livio sesión es eliminado (reinicio de clúster, etc.), no será capaz de toorun trabajos desde el Bloc de notas de hello Zeppeling.</span><span class="sxs-lookup"><span data-stu-id="e73ed-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="e73ed-193">En tal caso, debe realizar Hola siguiendo los pasos antes de empezar a ejecutar trabajos de un bloc de notas de Zeppeling.</span><span class="sxs-lookup"><span data-stu-id="e73ed-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="e73ed-194">Reinicie Hola intérprete Livio desde el Bloc de notas de hello Zeppeling.</span><span class="sxs-lookup"><span data-stu-id="e73ed-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="e73ed-195">toodo, abra Configuración de intérprete haciendo clic en hello registra en nombre de usuario desde la esquina superior derecha de hello y, a continuación, haga clic en **intérprete**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="e73ed-196">![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")</span><span class="sxs-lookup"><span data-stu-id="e73ed-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="e73ed-197">Desplácese tooLivy configuración de intérprete y, a continuación, haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="e73ed-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="e73ed-198">![Reinicie Hola Livio intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar hello Zeppeling intepreter")</span><span class="sxs-lookup"><span data-stu-id="e73ed-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="e73ed-199">Ejecute una celda de código desde el cuaderno de Zeppelin Notebook existente.</span><span class="sxs-lookup"><span data-stu-id="e73ed-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="e73ed-200">Esto crea una nueva sesión de Livio en clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="e73ed-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="e73ed-201"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e73ed-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e73ed-202">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e73ed-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="e73ed-203">Escenarios</span><span class="sxs-lookup"><span data-stu-id="e73ed-203">Scenarios</span></span>
* [<span data-ttu-id="e73ed-204">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="e73ed-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e73ed-205">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e73ed-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e73ed-206">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="e73ed-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e73ed-207">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="e73ed-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e73ed-208">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e73ed-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e73ed-209">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e73ed-209">Create and run applications</span></span>
* [<span data-ttu-id="e73ed-210">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="e73ed-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e73ed-211">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="e73ed-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e73ed-212">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="e73ed-212">Tools and extensions</span></span>
* [<span data-ttu-id="e73ed-213">Usar el complemento de herramientas de HDInsight para toocreate IntelliJ IDEA y enviar Spark Scala aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e73ed-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e73ed-214">Usar complemento Herramientas de HDInsight para aplicaciones de IDEA IntelliJ toodebug Spark de forma remota</span><span class="sxs-lookup"><span data-stu-id="e73ed-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e73ed-215">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="e73ed-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e73ed-216">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="e73ed-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e73ed-217">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e73ed-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e73ed-218">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="e73ed-218">Manage resources</span></span>
* [<span data-ttu-id="e73ed-219">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="e73ed-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e73ed-220">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="e73ed-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







