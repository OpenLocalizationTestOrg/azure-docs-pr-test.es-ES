---
title: "datos de tooanalyze Apache Spark en almacén de Azure Data Lake aaaUse | Documentos de Microsoft"
description: "Ejecutar trabajos de Spark tooanalyze los datos almacenados en el almacén de Azure Data Lake"
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
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="6d149-103">Usar datos de tooanalyze de clúster de HDInsight Spark en almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="6d149-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="6d149-104">En este tutorial, utilizará Jupyter notebook disponible con clústeres de HDInsight Spark toorun un trabajo que lee los datos de una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6d149-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d149-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6d149-105">Prerequisites</span></span>

* <span data-ttu-id="6d149-106">Cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6d149-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="6d149-107">Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6d149-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="6d149-108">Clúster de Azure HDInsight Spark con Data Lake Store como almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="6d149-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="6d149-109">Siga las instrucciones de hello en [crear un clúster de HDInsight con el almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6d149-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="6d149-110">Preparar los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="6d149-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="6d149-111">No es necesario tooperform en este paso si ha creado el clúster de HDInsight de hello con almacén de Data Lake como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="6d149-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="6d149-112">procesos de creación de clúster de Hello agrega algunos datos de ejemplo en la cuenta de almacén de Data Lake Hola que especifique al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d149-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="6d149-113">Omitir la sección toohello [clúster Use HDInsight Spark con almacén de Data Lake](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="6d149-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="6d149-114">Si ha creado un clúster de HDInsight con el almacén de Data Lake como almacenamiento adicional y Blob de almacenamiento de Azure como almacenamiento predeterminado, primero debe copiar sobre algunos toohello de datos de ejemplo cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6d149-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="6d149-115">Puede usar datos de ejemplo de Hola de hello que BLOB de almacenamiento de Azure asociado con el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="6d149-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="6d149-116">Puede usar hello [ADLCopy herramienta](http://aka.ms/downloadadlcopy) toodo para.</span><span class="sxs-lookup"><span data-stu-id="6d149-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="6d149-117">Descargue e instale la herramienta de Hola desde el vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d149-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="6d149-118">Abra un símbolo del sistema y desplácese directorio toohello AdlCopy está instalado, por lo general `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="6d149-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="6d149-119">Ejecute hello después comando toocopy un blob en cuestión desde Hola origen contenedor tooa almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="6d149-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="6d149-120">Hola copia **HVAC.csv** archivo de datos de ejemplo de **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello cuenta de almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6d149-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="6d149-121">fragmento de código de Hello debería ser similar:</span><span class="sxs-lookup"><span data-stu-id="6d149-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="6d149-122">Asegúrese de que Hola archivo y nombres de ruta de acceso están en mayúsculas o minúsculas Hola.</span><span class="sxs-lookup"><span data-stu-id="6d149-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="6d149-123">Podrá tooenter solicitada credenciales Hola para Hola suscripción de Azure en la que dispone de su cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6d149-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="6d149-124">Verá un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="6d149-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="6d149-125">archivo de datos de Hello (**HVAC.csv**) se copiarán en una carpeta **/hvac** Hola cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6d149-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="6d149-126">Uso de un clúster de HDInsight Spark con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6d149-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="6d149-127">De hello [Portal de Azure](https://portal.azure.com/), desde el panel de inicio de hello, haga clic en icono de hello para el clúster de Spark (si anclarlo toohello panel de inicio).</span><span class="sxs-lookup"><span data-stu-id="6d149-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="6d149-128">También puede navegar clúster tooyour en **examinar todos los** > **clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6d149-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="6d149-129">En la hoja de clúster de Spark hello, haga clic en **vínculos rápidos**y, a continuación, desde hello **panel clúster** hoja, haga clic en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="6d149-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="6d149-130">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="6d149-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6d149-131">También puede tener acceso a Jupyter Notebook hello para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="6d149-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="6d149-132">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="6d149-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="6d149-133">Cree un nuevo notebook.</span><span class="sxs-lookup"><span data-stu-id="6d149-133">Create a new notebook.</span></span> <span data-ttu-id="6d149-134">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="6d149-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="6d149-135">![Crear un nuevo cuaderno de Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Crear un nuevo cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="6d149-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="6d149-136">Como ha creado un bloc de notas con kernel PySpark de hello, no es necesario toocreate ningún contexto explícitamente.</span><span class="sxs-lookup"><span data-stu-id="6d149-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="6d149-137">contextos de Spark y Hive Hola se crearán automáticamente automáticamente cuando se ejecuta la primera celda de código de hello.</span><span class="sxs-lookup"><span data-stu-id="6d149-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="6d149-138">Puede iniciar mediante la importación de tipos de hello necesarios para este escenario.</span><span class="sxs-lookup"><span data-stu-id="6d149-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="6d149-139">toodo por lo tanto, pegue Hola siguiente fragmento de código en una celda y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="6d149-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="6d149-140">Cada vez que ejecute un trabajo en Jupyter, el título de ventana del explorador web le mostrará un **(estado ocupado)** estado junto con el título de hello Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="6d149-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="6d149-141">También verá un toohello siguiente círculo sólido **PySpark** texto en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d149-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="6d149-142">Una vez completado el trabajo de hello, esto también cambiará círculo hueco tooa.</span><span class="sxs-lookup"><span data-stu-id="6d149-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="6d149-143">![Estado de un trabajo de cuaderno de Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Estado de un trabajo de cuaderno de Jupyter")</span><span class="sxs-lookup"><span data-stu-id="6d149-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="6d149-144">Cargar datos de ejemplo en una tabla temporal con hello **HVAC.csv** archivo copiado toohello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6d149-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="6d149-145">Puede tener acceso a datos de hello en la cuenta de almacén de Data Lake de hello mediante Hola siguiendo el modelo de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="6d149-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="6d149-146">Si dispone de almacén de Data Lake como almacenamiento predeterminado, HVAC.csv estará en toohello similar en la ruta de acceso de hello después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="6d149-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="6d149-147">O bien, también podría utilizar un formato abreviado como siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6d149-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="6d149-148">Si dispone de almacén de Data Lake como almacenamiento adicional, HVAC.csv estará en hello ubicación donde haya copiado, como:</span><span class="sxs-lookup"><span data-stu-id="6d149-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="6d149-149">En una celda vacía, Hola pegar siguiente ejemplo de código, reemplace **MYDATALAKESTORE** con el nombre de la cuenta de almacén de Data Lake y presione **MAYÚS + ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="6d149-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="6d149-150">Este ejemplo de código registra datos de hello en una tabla temporal denominada **hvac**.</span><span class="sxs-lookup"><span data-stu-id="6d149-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="6d149-151">Puesto que está utilizando un núcleo de PySpark, ahora puede ejecutar directamente una consulta SQL en la tabla temporal de Hola **hvac** que acaba de crear mediante el uso de hello `%%sql` magia.</span><span class="sxs-lookup"><span data-stu-id="6d149-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="6d149-152">Para obtener más información acerca de hello `%%sql` mágico, así como otros magics disponibles con kernel PySpark de hello, consulte [núcleos disponibles en los equipos portátiles Jupyter con clústeres de HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="6d149-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="6d149-153">Una vez que se complete correctamente el trabajo de hello, Hola siguiendo la salida tabular se muestra de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6d149-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="6d149-154">![Salida de tabla del resultado de la consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Salida de tabla del resultado de la consulta")</span><span class="sxs-lookup"><span data-stu-id="6d149-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="6d149-155">También puede ver los resultados de hello en otras visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="6d149-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="6d149-156">Por ejemplo, un gráfico de áreas para hello misma salida sería Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="6d149-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="6d149-157">![Gráfico de área del resultado de la consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gráfico de área del resultado de la consulta")</span><span class="sxs-lookup"><span data-stu-id="6d149-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="6d149-158">Una vez haya terminado de ejecutar la aplicación hello, debería recursos de hello toorelease de apagado Hola Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="6d149-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="6d149-159">toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.</span><span class="sxs-lookup"><span data-stu-id="6d149-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="6d149-160">Este se apagará y portátil de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="6d149-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6d149-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d149-161">Next steps</span></span>

* [<span data-ttu-id="6d149-162">Crear un toorun de aplicación independiente Scala en clúster de Apache Spark</span><span class="sxs-lookup"><span data-stu-id="6d149-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="6d149-163">Usar herramientas de HDInsight en el Kit de herramientas de Azure IntelliJ toocreate Spark para las aplicaciones de clúster de HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="6d149-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="6d149-164">Usar herramientas de HDInsight en el Kit de herramientas de Azure Eclipse toocreate Spark para las aplicaciones de clúster de HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="6d149-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
