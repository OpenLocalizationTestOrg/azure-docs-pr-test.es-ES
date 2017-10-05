---
title: "Uso de cuadernos de Zeppelin con un clúster Apache Spark en Azure HDInsight | Microsoft Docs"
description: "Instrucciones paso a paso sobre cómo usar cuadernos de Zeppelin con clústeres Apache Spark en Azure HDInsight."
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
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="a4208-103">Uso de cuadernos de Zeppelin con un clúster Apache Spark en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4208-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="a4208-104">Los clústeres Spark de HDInsight contienen cuadernos de Zeppelin Notebook que se pueden utilizar para ejecutar trabajos de Spark.</span><span class="sxs-lookup"><span data-stu-id="a4208-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="a4208-105">En este artículo, aprenderá a usar Zeppelin Notebook en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4208-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a4208-106">Los notebooks de Zeppelin están disponibles solo para Spark 1.6.3 en HDInsight 3.5 y Spark 2.1.0 en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="a4208-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="a4208-107">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="a4208-107">**Prerequisites:**</span></span>

* <span data-ttu-id="a4208-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4208-108">An Azure subscription.</span></span> <span data-ttu-id="a4208-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a4208-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="a4208-110">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4208-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a4208-111">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="a4208-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="a4208-112">Inicio de un cuaderno de Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="a4208-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="a4208-113">En la hoja del clúster Spark, haga clic en **Panel de clúster** y en **Zeppelin Notebook**.</span><span class="sxs-lookup"><span data-stu-id="a4208-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="a4208-114">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="a4208-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a4208-115">También puede comunicarse con su equipo portátil ligero Zeppelin en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a4208-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="a4208-116">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="a4208-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="a4208-117">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="a4208-117">Create a new notebook.</span></span> <span data-ttu-id="a4208-118">En el panel de encabezado, haga clic en **Cuaderno** y luego en **Create New Note** (Crear nota).</span><span class="sxs-lookup"><span data-stu-id="a4208-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="a4208-119">![Creación de un nuevo cuaderno de Zeppeling](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Creación de un nuevo cuaderno de Zeppeling")</span><span class="sxs-lookup"><span data-stu-id="a4208-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="a4208-120">Especifique un nombre para el cuaderno y haga clic en **Create Note** (Crear nota).</span><span class="sxs-lookup"><span data-stu-id="a4208-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="a4208-121">Por otro lado, asegúrese de que en el encabezado del cuaderno aparece el estado conectado.</span><span class="sxs-lookup"><span data-stu-id="a4208-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="a4208-122">Esto estado se indica mediante un punto verde que se encuentra en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="a4208-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="a4208-123">![Estado del cuaderno de Zeppeling](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Estado del cuaderno de Zeppeling")</span><span class="sxs-lookup"><span data-stu-id="a4208-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="a4208-124">Cargue los datos de ejemplo en una tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="a4208-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="a4208-125">Cuando crea un clúster Spark en HDInsight, el archivo de datos de ejemplo, **hvac.csv**, se copia en la cuenta de almacenamiento asociada en **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="a4208-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="a4208-126">En el párrafo vacío que se crea de manera predeterminada en el nuevo cuaderno, pegue el siguiente fragmento.</span><span class="sxs-lookup"><span data-stu-id="a4208-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
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
   
    <span data-ttu-id="a4208-127">Presione **MAYÚS+ENTRAR** o haga clic en el botón **Reproducir** del párrafo para ejecutar el fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="a4208-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="a4208-128">El estado en la esquina derecha del párrafo debería avanzar de READY (Listo), PENDING (Pendiente) o RUNNING (En ejecución) a FINISHED (Finalizado).</span><span class="sxs-lookup"><span data-stu-id="a4208-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="a4208-129">El resultado se muestra en la parte inferior del mismo párrafo.</span><span class="sxs-lookup"><span data-stu-id="a4208-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="a4208-130">La captura de pantalla es similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a4208-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="a4208-131">![Creación de una tabla temporal a partir de datos sin procesar](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Creación de una tabla temporal a partir de datos sin procesar")</span><span class="sxs-lookup"><span data-stu-id="a4208-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="a4208-132">También puede proporcionar un título para cada párrafo.</span><span class="sxs-lookup"><span data-stu-id="a4208-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="a4208-133">En la esquina derecha, haga clic en el icono **Configuración** y luego haga clic en **Mostrar título**.</span><span class="sxs-lookup"><span data-stu-id="a4208-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="a4208-134">Ahora puede ejecutar instrucciones Spark SQL en la tabla **hvac** .</span><span class="sxs-lookup"><span data-stu-id="a4208-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="a4208-135">Pegue la siguiente consulta en un nuevo párrafo.</span><span class="sxs-lookup"><span data-stu-id="a4208-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="a4208-136">La consulta recupera el identificador del edificio y la diferencia entre la temperatura objetivo y la real para cada edificio en una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="a4208-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="a4208-137">Presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="a4208-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="a4208-138">La instrucción **%sql** del principio le indica al cuaderno que utilice el intérprete de Livy Scala.</span><span class="sxs-lookup"><span data-stu-id="a4208-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="a4208-139">En la captura de pantalla siguiente se muestra el resultado.</span><span class="sxs-lookup"><span data-stu-id="a4208-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="a4208-140">![Ejecución de una instrucción Spark SQL mediante el cuaderno](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Ejecución de una instrucción Spark SQL mediante el cuaderno")</span><span class="sxs-lookup"><span data-stu-id="a4208-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="a4208-141">Haga clic en las opciones de presentación (resaltadas con el rectángulo) para alternar entre diferentes representaciones del mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="a4208-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="a4208-142">Haga clic en **Settings** (Configuración) para elegir qué constituye la clave y los valores de la salida.</span><span class="sxs-lookup"><span data-stu-id="a4208-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="a4208-143">En la captura de pantalla anterior se usa **buildingID** como clave y la media de **temp_diff** como valor.</span><span class="sxs-lookup"><span data-stu-id="a4208-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="a4208-144">También puede ejecutar instrucciones Spark SQL usando variables en la consulta.</span><span class="sxs-lookup"><span data-stu-id="a4208-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="a4208-145">El siguiente fragmento de código muestra cómo definir una variable, **Temp**, en la consulta con los valores posibles con los que quiere hacer la consulta.</span><span class="sxs-lookup"><span data-stu-id="a4208-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="a4208-146">Cuando ejecuta la consulta por primera vez, se rellena una lista desplegable automáticamente con los valores especificados para la variable.</span><span class="sxs-lookup"><span data-stu-id="a4208-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="a4208-147">Pegue este fragmento de código en un nuevo párrafo y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="a4208-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="a4208-148">En la captura de pantalla siguiente se muestra el resultado.</span><span class="sxs-lookup"><span data-stu-id="a4208-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="a4208-149">![Ejecución de una instrucción Spark SQL mediante el cuaderno](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Ejecución de una instrucción Spark SQL mediante el cuaderno")</span><span class="sxs-lookup"><span data-stu-id="a4208-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="a4208-150">Para las consultas posteriores, puede seleccionar un nuevo valor en la lista desplegable y después volver a ejecutar la consulta.</span><span class="sxs-lookup"><span data-stu-id="a4208-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="a4208-151">Haga clic en **Settings** (Configuración) para elegir qué constituye la clave y los valores de la salida.</span><span class="sxs-lookup"><span data-stu-id="a4208-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="a4208-152">La captura de pantalla anterior usa **buildingID** como clave, la media de **temp_diff** como valor y **targettemp** como grupo.</span><span class="sxs-lookup"><span data-stu-id="a4208-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="a4208-153">Reinicie el intérprete de Livy para salir de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a4208-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="a4208-154">Para ello, abra la configuración del intérprete haciendo clic en el nombre del usuario conectado que encontrará en la esquina superior derecha y después en **Interpreter** (Intérprete).</span><span class="sxs-lookup"><span data-stu-id="a4208-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="a4208-155">![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")</span><span class="sxs-lookup"><span data-stu-id="a4208-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="a4208-156">Desplácese hasta la configuración del intérprete de Livy y haga clic en **Restart** (Reiniciar).</span><span class="sxs-lookup"><span data-stu-id="a4208-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="a4208-157">![Reinicio del intérprete de Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Reinicio del intérprete de Zeppeling")</span><span class="sxs-lookup"><span data-stu-id="a4208-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="a4208-158">Uso de paquetes externos con el cuaderno</span><span class="sxs-lookup"><span data-stu-id="a4208-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="a4208-159">Puede configurar el cuaderno de Zeppelin Notebook en un clúster Apache Spark de HDInsight (Linux) si desea usar paquetes externos aportados por la comunidad que no estén incluidos en el clúster.</span><span class="sxs-lookup"><span data-stu-id="a4208-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="a4208-160">Puede buscar el [repositorio de Maven](http://search.maven.org/) para obtener una lista completa de los paquetes que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="a4208-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="a4208-161">También puede obtener una lista de paquetes disponibles de otras fuentes.</span><span class="sxs-lookup"><span data-stu-id="a4208-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="a4208-162">Por ejemplo, dispone de la lista completa de los paquetes externos aportados por la comunidad en [Spark Packages](http://spark-packages.org/)(Paquetes Spark).</span><span class="sxs-lookup"><span data-stu-id="a4208-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="a4208-163">En este artículo, aprenderá a utilizar el paquete [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) con el cuaderno de Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="a4208-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="a4208-164">Abra la configuración del intérprete.</span><span class="sxs-lookup"><span data-stu-id="a4208-164">Open interpreter settings.</span></span> <span data-ttu-id="a4208-165">En la esquina superior derecha, haga clic en el nombre del usuario conectado y en **Interpreter** (Intérprete).</span><span class="sxs-lookup"><span data-stu-id="a4208-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="a4208-166">![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")</span><span class="sxs-lookup"><span data-stu-id="a4208-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="a4208-167">Desplácese hasta la configuración del intérprete de Livy y haga clic en **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="a4208-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="a4208-168">![Cambio de la configuración del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Cambio de la configuración del intérprete")</span><span class="sxs-lookup"><span data-stu-id="a4208-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="a4208-169">Agregue la nueva clave **livy.spark.jars.packages** y establezca su valor con el formato `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="a4208-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="a4208-170">Por ejemplo, si desea usar el paquete [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar), debe establecer el valor de la clave en `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="a4208-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="a4208-171">![Cambio de la configuración del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Cambio de la configuración del intérprete")</span><span class="sxs-lookup"><span data-stu-id="a4208-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="a4208-172">Haga clic en **Save** (Guardar) y reinicie el intérprete de Livy.</span><span class="sxs-lookup"><span data-stu-id="a4208-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="a4208-173">**Sugerencia**: Si desea saber cómo acceder al valor de la clave especificada anteriormente, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="a4208-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="a4208-174">a.</span><span class="sxs-lookup"><span data-stu-id="a4208-174">a.</span></span> <span data-ttu-id="a4208-175">Busque el paquete en el repositorio de Maven.</span><span class="sxs-lookup"><span data-stu-id="a4208-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="a4208-176">En este tutorial, hemos utilizado [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="a4208-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="a4208-177">b.</span><span class="sxs-lookup"><span data-stu-id="a4208-177">b.</span></span> <span data-ttu-id="a4208-178">En el repositorio, recopile los valores de **GroupId**, **ArtifactId** y **Version**.</span><span class="sxs-lookup"><span data-stu-id="a4208-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="a4208-179">![Uso de paquetes externos con cuadernos de Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Uso de paquetes externos con cuadernos de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="a4208-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="a4208-180">c.</span><span class="sxs-lookup"><span data-stu-id="a4208-180">c.</span></span> <span data-ttu-id="a4208-181">Concatene los tres valores separados por dos puntos (**:**).</span><span class="sxs-lookup"><span data-stu-id="a4208-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="a4208-182">¿Dónde se guardan los cuadernos de Zeppelin Notebook?</span><span class="sxs-lookup"><span data-stu-id="a4208-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="a4208-183">Los cuadernos de Zeppelin Notebook se guardan en los nodos principales del clúster.</span><span class="sxs-lookup"><span data-stu-id="a4208-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="a4208-184">Por tanto, si se elimina el clúster, también se eliminarán los cuadernos.</span><span class="sxs-lookup"><span data-stu-id="a4208-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="a4208-185">Si desea guardar los cuadernos para utilizarlos más adelante en otros clústeres, debe exportarlos cuando haya terminado de ejecutar los trabajos.</span><span class="sxs-lookup"><span data-stu-id="a4208-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="a4208-186">Para exportar un cuaderno, haga clic en el icono **Export** (Exportar), tal y como se muestra en la ilustración siguiente.</span><span class="sxs-lookup"><span data-stu-id="a4208-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="a4208-187">![Descarga del cuaderno](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Descarga del cuaderno")</span><span class="sxs-lookup"><span data-stu-id="a4208-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="a4208-188">De este modo, el cuaderno se guarda como un archivo JSON en la ubicación de descarga.</span><span class="sxs-lookup"><span data-stu-id="a4208-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="a4208-189">Administración de sesiones de Livy</span><span class="sxs-lookup"><span data-stu-id="a4208-189">Livy session management</span></span>
<span data-ttu-id="a4208-190">Cuando ejecute el primer párrafo de código del cuaderno de Zeppelin Notebook, se creará una nueva sesión de Livy en el clúster Spark de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4208-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="a4208-191">Esta sesión se compartirá con todos los cuadernos de Zeppelin Notebook que cree en el futuro.</span><span class="sxs-lookup"><span data-stu-id="a4208-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="a4208-192">Si, por alguna razón, termina la sesión de Livy (por ejemplo, se reinicia el clúster), no podrá ejecutar trabajos desde el cuaderno de Zeppelin Notebook.</span><span class="sxs-lookup"><span data-stu-id="a4208-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="a4208-193">En este caso, debe seguir los pasos que se indican a continuación para poder ejecutar trabajos desde un cuaderno de Zeppelin Notebook.</span><span class="sxs-lookup"><span data-stu-id="a4208-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="a4208-194">Reinicie el intérprete de Livy desde el cuaderno de Zeppelin Notebook.</span><span class="sxs-lookup"><span data-stu-id="a4208-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="a4208-195">Para ello, abra la configuración del intérprete haciendo clic en el nombre del usuario conectado que encontrará en la esquina superior derecha y después en **Interpreter** (Intérprete).</span><span class="sxs-lookup"><span data-stu-id="a4208-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="a4208-196">![Inicio del intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Salida de Hive")</span><span class="sxs-lookup"><span data-stu-id="a4208-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="a4208-197">Desplácese hasta la configuración del intérprete de Livy y haga clic en **Restart** (Reiniciar).</span><span class="sxs-lookup"><span data-stu-id="a4208-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="a4208-198">![Reinicio del intérprete de Livy](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Reinicio del intérprete de Zeppeling")</span><span class="sxs-lookup"><span data-stu-id="a4208-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="a4208-199">Ejecute una celda de código desde el cuaderno de Zeppelin Notebook existente.</span><span class="sxs-lookup"><span data-stu-id="a4208-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="a4208-200">Esto creará una nueva sesión de Livy en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4208-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="a4208-201"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a4208-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a4208-202">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="a4208-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="a4208-203">Escenarios</span><span class="sxs-lookup"><span data-stu-id="a4208-203">Scenarios</span></span>
* [<span data-ttu-id="a4208-204">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="a4208-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a4208-205">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="a4208-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a4208-206">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="a4208-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a4208-207">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="a4208-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a4208-208">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4208-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a4208-209">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a4208-209">Create and run applications</span></span>
* [<span data-ttu-id="a4208-210">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="a4208-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a4208-211">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="a4208-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a4208-212">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="a4208-212">Tools and extensions</span></span>
* [<span data-ttu-id="a4208-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para crear y enviar aplicaciones Scala Spark)</span><span class="sxs-lookup"><span data-stu-id="a4208-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a4208-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Uso del complemento de herramientas de HDInsight para IntelliJ IDEA para depurar aplicaciones de Spark de forma remota)</span><span class="sxs-lookup"><span data-stu-id="a4208-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="a4208-215">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4208-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a4208-216">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="a4208-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="a4208-217">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="a4208-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a4208-218">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="a4208-218">Manage resources</span></span>
* [<span data-ttu-id="a4208-219">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="a4208-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a4208-220">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="a4208-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







