---
title: "Creación de un clúster de Apache Spark en Azure HDInsight | Microsoft Docs"
description: "Tutorial de inicio rápido para HDInsight Spark sobre cómo crear un clúster de Apache Spark en HDInsight."
keywords: "inicio rápido para spark,spark interactivo,consulta interactiva,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ad4330a1fc7f8de154d9aaa8df3acc2ab59b9dc1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="dda11-104">Creación de un clúster de Apache Spark en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dda11-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="dda11-105">En este artículo, aprenderá a crear un clúster de Apache Spark en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dda11-105">In this article, you learn how to create an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="dda11-106">Para obtener información sobre Spark en HDInsight, consulte [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dda11-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="dda11-107">![Diagrama de inicio rápido donde se describen los pasos para crear un clúster de Apache Spark en Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Inicio rápido para Spark mediante Apache Spark en HDInsight. Pasos que ilustran cómo crear un clúster y ejecutar una consulta Spark interactiva")</span><span class="sxs-lookup"><span data-stu-id="dda11-107">![Quickstart diagram describing steps to create an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dda11-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dda11-108">Prerequisites</span></span>

* <span data-ttu-id="dda11-109">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="dda11-109">**An Azure subscription**.</span></span> <span data-ttu-id="dda11-110">Antes de comenzar este tutorial, debe tener una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="dda11-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="dda11-111">Consulte la página [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="dda11-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="dda11-112">Creación de un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="dda11-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="dda11-113">En esta sección, creará un clúster de HDInsight Spark mediante una [plantilla de Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="dda11-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="dda11-114">Para conocer otros métodos de creación de clústeres, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="dda11-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="dda11-115">Haga clic en la imagen siguiente para abrir la plantilla en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dda11-115">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="dda11-116">Escriba los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="dda11-116">Enter the following values:</span></span>

    <span data-ttu-id="dda11-117">![Creación de un clúster de HDInsight Spark mediante una plantilla de Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Creación de un clúster de HDInsight Spark mediante una plantilla de Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="dda11-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="dda11-118">**Suscripción**: seleccione su suscripción de Azure para este clúster.</span><span class="sxs-lookup"><span data-stu-id="dda11-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="dda11-119">**Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="dda11-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="dda11-120">El grupo de recursos se usa para administrar los recursos de Azure para sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="dda11-120">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="dda11-121">**Ubicación**: seleccione una ubicación para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dda11-121">**Location**: Select a location for the resource group.</span></span> <span data-ttu-id="dda11-122">La plantilla utiliza esta ubicación para crear el clúster, así como para el almacenamiento de clúster predeterminado.</span><span class="sxs-lookup"><span data-stu-id="dda11-122">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span>
    * <span data-ttu-id="dda11-123">**Nombre del clúster**: escriba un nombre para el clúster de HDInsight que va a crear.</span><span class="sxs-lookup"><span data-stu-id="dda11-123">**ClusterName**: Enter a name for the HDInsight cluster that you want to create.</span></span>
    * <span data-ttu-id="dda11-124">**Versión de Spark**: seleccione **2.0** como la versión de Spark que quiere instalar en el clúster.</span><span class="sxs-lookup"><span data-stu-id="dda11-124">**Spark version**: Select **2.0** as the version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="dda11-125">**Nombre de inicio de sesión y contraseña de clúster**: el nombre de inicio de sesión predeterminado es admin.</span><span class="sxs-lookup"><span data-stu-id="dda11-125">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="dda11-126">**Nombre de usuario y contraseña de SSH**.</span><span class="sxs-lookup"><span data-stu-id="dda11-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="dda11-127">Anote estos valores.</span><span class="sxs-lookup"><span data-stu-id="dda11-127">Write down these values.</span></span>  <span data-ttu-id="dda11-128">Los necesitará más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="dda11-128">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="dda11-129">Seleccione **I agree to the terms and conditions stated above** (Acepto los términos y condiciones indicados anteriormente) y **Anclar al panel** y haga clic en **Purchase** (Comprar).</span><span class="sxs-lookup"><span data-stu-id="dda11-129">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="dda11-130">Puede ver un icono nuevo llamado Envío de implementación para la implementación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="dda11-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="dda11-131">La creación del clúster tarda aproximadamente 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="dda11-131">It takes about 20 minutes to create the cluster.</span></span>

<span data-ttu-id="dda11-132">Si surge un problema con la creación de clústeres de HDInsight, podría deberse a que no tiene los permisos adecuados para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="dda11-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="dda11-133">Consulte [Requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters) para más información.</span><span class="sxs-lookup"><span data-stu-id="dda11-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="dda11-134">En este artículo se crea un clúster de Spark que usa [blobs de Azure Storage como almacenamiento](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dda11-134">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="dda11-135">También puede crear un clúster de Spark que use [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) como almacenamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="dda11-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as the default storage.</span></span> <span data-ttu-id="dda11-136">Consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dda11-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="dda11-137">Ejecución de una consulta de Hive con Spark SQL</span><span class="sxs-lookup"><span data-stu-id="dda11-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="dda11-138">Cuando se utiliza un cuaderno de Jupyter Notebook configurado para el clúster de HDInsight Spark, obtendrá un valor `sqlContext` preestablecido que puede usar para ejecutar consultas de Hive con Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="dda11-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="dda11-139">En esta sección, aprenderá a iniciar un cuaderno de Jupyter Notebook y después a ejecutar una consulta de Hive básica.</span><span class="sxs-lookup"><span data-stu-id="dda11-139">In this section, you learn how to start a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="dda11-140">Abra el [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dda11-140">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="dda11-141">Si ha elegido anclar el clúster al panel, haga clic en el icono de clúster desde el panel para abrir la hoja del clúster.</span><span class="sxs-lookup"><span data-stu-id="dda11-141">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="dda11-142">Si no ancló el clúster al panel, en el panel izquierdo, haga clic en **Clústeres de HDInsight** y luego haga clic en el clúster que ha creado.</span><span class="sxs-lookup"><span data-stu-id="dda11-142">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="dda11-143">En **Quick links** (Vínculos rápidos), haga clic en **Cluster dashboards** (Paneles de clúster) y después en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="dda11-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="dda11-144">Cuando se le pida, escriba las credenciales del clúster.</span><span class="sxs-lookup"><span data-stu-id="dda11-144">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="dda11-145">![Abrir un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Abrir un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas")</span><span class="sxs-lookup"><span data-stu-id="dda11-145">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="dda11-146">También puede acceder al cuaderno de Jupyter en el clúster si abre la siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="dda11-146">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="dda11-147">Reemplace **CLUSTERNAME** por el nombre del clúster:</span><span class="sxs-lookup"><span data-stu-id="dda11-147">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="dda11-148">Cree un cuaderno.</span><span class="sxs-lookup"><span data-stu-id="dda11-148">Create a notebook.</span></span> <span data-ttu-id="dda11-149">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="dda11-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="dda11-150">![Crear un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Crear un cuaderno de Jupyter para ejecutar consultas Spark SQL interactivas")</span><span class="sxs-lookup"><span data-stu-id="dda11-150">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="dda11-151">Se crea y se abre un nuevo Notebook con el nombre Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="dda11-151">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="dda11-152">Haga clic en el nombre del Notebook en la parte superior y escriba un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="dda11-152">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="dda11-153">![Proporcionar un nombre para el cuaderno de Jupyter para ejecutar consultas Spark interactivas](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Proporcionar un nombre para el cuaderno de Jupyter ejecutar consultas Spark interactivas")</span><span class="sxs-lookup"><span data-stu-id="dda11-153">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5.  <span data-ttu-id="dda11-154">Pegue el código siguiente en una celda vacía y presione **MAYÚS + ENTRAR** para ejecutar el código.</span><span class="sxs-lookup"><span data-stu-id="dda11-154">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="dda11-155">En el código siguiente `%%sql` (denominado instrucción mágica de SQL) indica a un cuaderno de Jupyter Notebook que utilice el valor `sqlContext` predeterminado para ejecutar la consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="dda11-155">In the code below `%%sql` (called the sql magic) tells Jupyter notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="dda11-156">La consulta recupera las 10 primeras filas de una tabla de Hive (**hivesampletable**) que está disponible de forma predeterminada en todos los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dda11-156">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="dda11-157">![Consulta de Hive en HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Consulta de Hive en HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="dda11-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="dda11-158">Para más información sobre las `%%sql` instrucciones mágicas y los contextos preestablecidos, consulte [Kernels para Jupyter Notebook en clústeres Spark en Azure HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="dda11-158">For more information on the `%%sql` magic and the preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="dda11-159">Cada vez que se ejecuta una consulta en Jupyter, el título de la ventana del explorador web muestra el estado **(Busy)** (Ocupado) junto con el título del Notebook.</span><span class="sxs-lookup"><span data-stu-id="dda11-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="dda11-160">También verá un círculo sólido junto al texto **PySpark** en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="dda11-160">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="dda11-161">Cuando finaliza el trabajo, cambia a un círculo vacío.</span><span class="sxs-lookup"><span data-stu-id="dda11-161">After the job is completed, it changes to a hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="dda11-162">Debe actualizar la pantalla para mostrar el resultado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="dda11-162">The screen should refresh to show the query output.</span></span>

    <span data-ttu-id="dda11-163">![Consulta de Hive en HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Consulta de Hive en HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="dda11-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="dda11-164">Cuando haya terminado de ejecutar la aplicación, cierre el Notebook para liberar los recursos del clúster.</span><span class="sxs-lookup"><span data-stu-id="dda11-164">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="dda11-165">Para ello, en el menú **Archivo** del cuaderno, haga clic en **Cerrar y detener**.</span><span class="sxs-lookup"><span data-stu-id="dda11-165">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="dda11-166">Si tiene previsto completar los pasos siguientes en otro momento, asegúrese de eliminar el clúster de HDInsight que creó en este artículo.</span><span class="sxs-lookup"><span data-stu-id="dda11-166">If you plan to complete the next steps at a later time, make sure you delete the HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="dda11-167">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="dda11-167">Next step</span></span> 

<span data-ttu-id="dda11-168">En este artículo ha aprendido a crear un clúster de HDInsight Spark y a ejecutar una consulta básica de Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="dda11-168">In this article you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="dda11-169">Continúe hasta el siguiente artículo para obtener información sobre cómo usar un clúster de HDInsight Spark para ejecutar consultas interactivas en datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="dda11-169">Advance to the next article to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="dda11-170">Ejecución de consultas interactivas en un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="dda11-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



