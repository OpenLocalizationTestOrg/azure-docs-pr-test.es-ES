---
title: Uso de Apache Spark para analizar datos en Azure Data Lake Store | Microsoft Docs
description: "Ejecución de trabajos de Spark para analizar los datos almacenados en Azure Data Lake Store"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="af0d0-103">Uso de un clúster de HDInsight Spark para analizar los datos en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="af0d0-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="af0d0-104">En este tutorial usará Jupyter Notebook, disponible con los clústeres de HDInsight Spark, para ejecutar un trabajo que lee datos de una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af0d0-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af0d0-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="af0d0-105">Prerequisites</span></span>

* <span data-ttu-id="af0d0-106">Cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af0d0-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="af0d0-107">Siga las instrucciones que se describen en [Introducción al Almacén de Azure Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af0d0-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="af0d0-108">Clúster de Azure HDInsight Spark con Data Lake Store como almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af0d0-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="af0d0-109">Consulte las instrucciones que se indican en [Creación de un clúster de HDInsight con Data Lake Store mediante Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af0d0-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="af0d0-110">Preparación de los datos</span><span class="sxs-lookup"><span data-stu-id="af0d0-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="af0d0-111">No hay que realizar este paso si ha creado el clúster de HDInsight con Data Lake Store como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="af0d0-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="af0d0-112">La creación del clúster agrega algunos datos de ejemplo en la cuenta de Data Lake Store especificados durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="af0d0-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="af0d0-113">Avance a la sección [Uso de un clúster de HDInsight Spark con Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="af0d0-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="af0d0-114">Si ha creado un clúster de HDInsight con Data Lake Store como almacenamiento adicional y Azure Storage Blob como almacenamiento predeterminado, primero debe copiar algunos datos de ejemplo en la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af0d0-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="af0d0-115">Puede usar los datos de ejemplo de la instancia de Azure Storage Blob asociada al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af0d0-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="af0d0-116">Puede usar la [herramienta ADLCopy](http://aka.ms/downloadadlcopy) para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="af0d0-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="af0d0-117">Descargue e instale la herramienta desde el vínculo.</span><span class="sxs-lookup"><span data-stu-id="af0d0-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="af0d0-118">Abra un símbolo del sistema y vaya al directorio donde está instalada la herramienta AdlCopy, normalmente `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="af0d0-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="af0d0-119">Ejecute el siguiente comando para copiar un blob específico desde el contenedor de origen a un Almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="af0d0-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="af0d0-120">Copie el archivo de datos de ejemplo **HVAC.csv** situado en **/HdiSamples/HdiSamples/SensorSampleData/hvac/** en la cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af0d0-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="af0d0-121">El fragmento de código debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="af0d0-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="af0d0-122">Asegúrese de que coincida el uso de mayúsculas y minúsculas en los nombres de archivo y ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="af0d0-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="af0d0-123">Se le pedirá que escriba las credenciales de la suscripción a Azure en la que tiene la cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af0d0-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="af0d0-124">Verá un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="af0d0-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="af0d0-125">El archivo de datos (**HVAC.csv**) se copiará en una carpeta **/hvac** en la cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af0d0-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="af0d0-126">Uso de un clúster de HDInsight Spark con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="af0d0-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="af0d0-127">Desde el [Portal de Azure](https://portal.azure.com/), en el panel de inicio, haga clic en el icono del clúster Spark (si lo ancló al panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="af0d0-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="af0d0-128">También puede navegar hasta el clúster en **Examinar todo** > **Clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="af0d0-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="af0d0-129">En la hoja del clúster Spark, haga clic en **Vínculos rápidos** y, luego, en la hoja **Panel de clúster**, haga clic en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="af0d0-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="af0d0-130">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="af0d0-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="af0d0-131">También puede comunicarse con el equipo Jupyter Notebook en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="af0d0-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="af0d0-132">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="af0d0-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="af0d0-133">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="af0d0-133">Create a new notebook.</span></span> <span data-ttu-id="af0d0-134">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="af0d0-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="af0d0-135">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="af0d0-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="af0d0-136">Dado que creó un cuaderno con el kernel PySpark, no necesitará crear ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="af0d0-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="af0d0-137">Los contextos Spark y Hive se crearán automáticamente al ejecutar la primera celda de código.</span><span class="sxs-lookup"><span data-stu-id="af0d0-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="af0d0-138">Puede empezar por importar los tipos necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="af0d0-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="af0d0-139">Para ello, pegue el siguiente fragmento de código en una celda y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="af0d0-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="af0d0-140">Cada vez que se ejecuta un trabajo en Jupyter, el título de la ventana del explorador web mostrará el estado **(Busy)** (Ocupado) junto con el título del cuaderno.</span><span class="sxs-lookup"><span data-stu-id="af0d0-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="af0d0-141">También verá un círculo sólido junto al texto **PySpark** en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="af0d0-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="af0d0-142">Una vez completado el trabajo, cambiará a un círculo hueco.</span><span class="sxs-lookup"><span data-stu-id="af0d0-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="af0d0-143">![Estado de un trabajo de cuaderno de Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Estado de un trabajo de cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="af0d0-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="af0d0-144">Cargue datos de ejemplo en una tabla temporal mediante el archivo **HVAC.csv** que copió a la cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="af0d0-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="af0d0-145">Ahora puede acceder a los datos de la cuenta del Almacén de Data Lake con el siguiente patrón de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="af0d0-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="af0d0-146">Si dispone de Data Lake Store como almacenamiento predeterminado, HVAC.csv estará en la ruta de acceso similar a la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="af0d0-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="af0d0-147">También podría usar un formato abreviado como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="af0d0-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="af0d0-148">Si cuenta con Data Lake Store como almacenamiento adicional, HVAC.csv estará en la ubicación donde lo copió, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="af0d0-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="af0d0-149">En una celda vacía, pegue el siguiente ejemplo de código, reemplace **MYDATALAKESTORE** por el nombre de su cuenta de Azure Data Lake Store y presione **MAYÚS+ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="af0d0-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="af0d0-150">Este ejemplo de código registra los datos en una tabla temporal llamada **hvac**.</span><span class="sxs-lookup"><span data-stu-id="af0d0-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="af0d0-151">Al usar un kernel de PySpark, puede ejecutar directamente una consulta SQL en la tabla temporal **hvac** que acaba de crear con la instrucción mágica `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="af0d0-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="af0d0-152">Para obtener más información sobre la función mágica `%%sql` , así como otras función mágicas disponibles con el kernel de PySpark, vea [Kernels disponibles para cuadernos de Jupyter con clústeres Spark en HDInsight (Linux)](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="af0d0-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="af0d0-153">Una vez que el trabajo se completa correctamente, se muestra de forma predeterminada el resultado tabular siguiente.</span><span class="sxs-lookup"><span data-stu-id="af0d0-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="af0d0-154">![Salida de tabla del resultado de la consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Salida de tabla del resultado de la consulta")</span><span class="sxs-lookup"><span data-stu-id="af0d0-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="af0d0-155">También puede ver la salida en otras visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="af0d0-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="af0d0-156">Por ejemplo, un gráfico de área con la misma salida tendría el siguiente aspecto.</span><span class="sxs-lookup"><span data-stu-id="af0d0-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="af0d0-157">![Gráfico de área del resultado de la consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gráfico de área del resultado de la consulta")</span><span class="sxs-lookup"><span data-stu-id="af0d0-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="af0d0-158">Cuando haya terminado de ejecutar la aplicación, debe cerrar el cuaderno para liberar los recursos.</span><span class="sxs-lookup"><span data-stu-id="af0d0-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="af0d0-159">Para ello, en el menú **Archivo** del cuaderno, haga clic en **Cerrar y detener**.</span><span class="sxs-lookup"><span data-stu-id="af0d0-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="af0d0-160">De esta manera se apagará y se cerrará el cuaderno.</span><span class="sxs-lookup"><span data-stu-id="af0d0-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="af0d0-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af0d0-161">Next steps</span></span>

* [<span data-ttu-id="af0d0-162">Creación de una aplicación independiente con Scala para ejecutarla en un clúster de Apache Spark</span><span class="sxs-lookup"><span data-stu-id="af0d0-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="af0d0-163">Uso de las herramientas de HDInsight del kit de herramientas de Azure para IntelliJ con el fin de crear aplicaciones Spark destinadas al clúster Spark en HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="af0d0-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="af0d0-164">Uso de las herramientas de HDInsight del kit de herramientas de Azure para Eclipse con el fin de crear aplicaciones Spark destinadas al clúster Spark en HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="af0d0-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
