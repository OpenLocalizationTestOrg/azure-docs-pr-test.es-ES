---
title: "clúster de aaaCreate un Apache Spark en HDInsight de Azure | Documentos de Microsoft"
description: "Inicio rápido de HDInsight Spark en forma de clúster toocreate un Apache Spark en HDInsight."
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
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="b8663-104">Creación de un clúster de Apache Spark en Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b8663-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="b8663-105">En este artículo, aprenderá cómo agrupar toocreate un Apache Spark en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8663-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="b8663-106">Para obtener información sobre Spark en HDInsight, consulte [Introducción a Apache Spark en HDInsight de Azure](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8663-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="b8663-107">![Diagrama de inicio rápido que describe los pasos toocreate un clúster de Apache Spark en HDInsight de Azure](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "inicio rápido de Spark con Apache Spark en HDInsight. Pasos que ilustran cómo crear un clúster y ejecutar una consulta Spark interactiva")</span><span class="sxs-lookup"><span data-stu-id="b8663-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8663-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b8663-108">Prerequisites</span></span>

* <span data-ttu-id="b8663-109">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b8663-109">**An Azure subscription**.</span></span> <span data-ttu-id="b8663-110">Antes de comenzar este tutorial, debe tener una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="b8663-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="b8663-111">Consulte la página [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b8663-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="b8663-112">Creación de un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b8663-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="b8663-113">En esta sección, creará un clúster de HDInsight Spark mediante una [plantilla de Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="b8663-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="b8663-114">Para conocer otros métodos de creación de clústeres, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b8663-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="b8663-115">Haga clic en hello después de la plantilla de imagen tooopen Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8663-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="b8663-116">Escriba Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="b8663-116">Enter hello following values:</span></span>

    <span data-ttu-id="b8663-117">![Creación de un clúster de HDInsight Spark mediante una plantilla de Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Creación de un clúster de HDInsight Spark mediante una plantilla de Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="b8663-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="b8663-118">**Suscripción**: seleccione su suscripción de Azure para este clúster.</span><span class="sxs-lookup"><span data-stu-id="b8663-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="b8663-119">**Grupo de recursos**: cree un grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="b8663-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="b8663-120">Grupo de recursos es toomanage usa recursos de Azure para sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="b8663-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="b8663-121">**Ubicación**: seleccione una ubicación para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="b8663-122">plantilla de Hello usa esta ubicación para crear clúster Hola así en cuanto al almacenamiento de clúster predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="b8663-123">**ClusterName**: escriba un nombre para el clúster de HDInsight de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="b8663-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="b8663-124">**Versión de Spark**: seleccione **2.0** como versión de Hola que desea tooinstall en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="b8663-125">**Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es administrador.</span><span class="sxs-lookup"><span data-stu-id="b8663-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="b8663-126">**Nombre de usuario y contraseña de SSH**.</span><span class="sxs-lookup"><span data-stu-id="b8663-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="b8663-127">Anote estos valores.</span><span class="sxs-lookup"><span data-stu-id="b8663-127">Write down these values.</span></span>  <span data-ttu-id="b8663-128">Se necesita más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="b8663-129">Seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**, seleccione **Pin toodashboard**y, a continuación, haga clic en **compra**.</span><span class="sxs-lookup"><span data-stu-id="b8663-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="b8663-130">Puede ver un icono nuevo llamado Envío de implementación para la implementación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="b8663-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="b8663-131">Toma clúster de hello toocreate alrededor de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="b8663-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="b8663-132">Si surge un problema con la creación de clústeres de HDInsight, podría deberse a que no tienen Hola permisos adecuados toodo por lo que.</span><span class="sxs-lookup"><span data-stu-id="b8663-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="b8663-133">Consulte [Requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters) para más información.</span><span class="sxs-lookup"><span data-stu-id="b8663-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="b8663-134">Este artículo crea un clúster de Spark que use [almacenamiento de Blobs de almacenamiento de Azure como Hola clúster](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b8663-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="b8663-135">También puede crear un clúster de Spark que use [almacén de Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md) como almacenamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="b8663-136">Consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b8663-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="b8663-137">Ejecución de una consulta de Hive con Spark SQL</span><span class="sxs-lookup"><span data-stu-id="b8663-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="b8663-138">Cuando usas configurado para el clúster de HDInsight Spark Jupyter notebook, obtendrá un valor preestablecido `sqlContext` que puede usar consultas de Hive toorun usar Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="b8663-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="b8663-139">En esta sección, aprenderá cómo toostart Jupyter notebook y, a continuación, ejecutar una consulta de Hive básica.</span><span class="sxs-lookup"><span data-stu-id="b8663-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="b8663-140">Abra hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b8663-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="b8663-141">Si ha elegido el panel de toohello de toopin Hola clúster, haga clic en icono de clúster de Hola desde la hoja de clúster de hello panel toolaunch Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="b8663-142">Si no ancla panel Hola clúster toohello, desde el panel izquierdo de hello, haga clic en **clústeres de HDInsight**y, a continuación, haga clic en clúster de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="b8663-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="b8663-143">En **Quick links** (Vínculos rápidos), haga clic en **Cluster dashboards** (Paneles de clúster) y después en **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="b8663-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="b8663-144">Si se le pide, escriba las credenciales de administrador de Hola para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="b8663-145">![Abrir Jupyter notebook toorun interactivo Spark SQL consulta](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "consultas Jupyter Abrir Bloc de notas toorun interactivo Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="b8663-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="b8663-146">También puede tener acceso a Jupyter notebook de hello para el clúster por abrir Hola siguiente dirección URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="b8663-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="b8663-147">Reemplace **CLUSTERNAME** con nombre hello del clúster:</span><span class="sxs-lookup"><span data-stu-id="b8663-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="b8663-148">Cree un cuaderno.</span><span class="sxs-lookup"><span data-stu-id="b8663-148">Create a notebook.</span></span> <span data-ttu-id="b8663-149">Haga clic en **Nuevo** y, luego, en **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="b8663-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="b8663-150">![Crear una consulta de Spark SQL interactiva de Jupyter notebook toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "crear una consulta Jupyter notebook toorun interactiva Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="b8663-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="b8663-151">Un nuevo bloc de notas se crea y se abre con el nombre de hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="b8663-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="b8663-152">Haga clic en nombre de Bloc de notas de hello en la parte superior de Hola y escriba un nombre descriptivo si desea.</span><span class="sxs-lookup"><span data-stu-id="b8663-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="b8663-153">![Proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva de](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "proporcione un nombre para hello Jupter Bloc de notas toorun Spark consulta interactiva desde")</span><span class="sxs-lookup"><span data-stu-id="b8663-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="b8663-154">Siguiente de Hola de pegar código en una celda vacía y, a continuación, presione **MAYÚS + ENTRAR** código de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="b8663-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="b8663-155">En el siguiente código de hello `%%sql` (mágico de sql llamado hello) indica preestablecido Hola de Jupyter notebook toouse `sqlContext` consulta de Hive toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="b8663-156">consulta de Hello recupera Hola 10 primeras filas de una tabla de Hive (**hivesampletable**) que está disponible de forma predeterminada en todos los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b8663-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="b8663-157">![Consulta de Hive en HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Consulta de Hive en HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="b8663-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="b8663-158">Para obtener más información sobre hello `%%sql` hello y magia preestablecido contextos, consulte [Jupyter núcleos disponibles para un clúster de HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="b8663-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b8663-159">Cada vez que ejecute una consulta en Jupyter, el título de ventana de explorador web muestra un **(estado ocupado)** estado junto con el título de hello Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="b8663-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="b8663-160">También verá un toohello siguiente círculo sólido **PySpark** texto en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="b8663-161">Una vez completado el trabajo de hello, cambia el círculo hueco tooa.</span><span class="sxs-lookup"><span data-stu-id="b8663-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="b8663-162">pantalla de bienvenida debe actualizar el resultado de la consulta de tooshow Hola.</span><span class="sxs-lookup"><span data-stu-id="b8663-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="b8663-163">![Consulta de Hive en HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Consulta de Hive en HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="b8663-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="b8663-164">Apagar los recursos de clúster de hello Bloc de notas toorelease Hola después de que haya terminado de ejecutar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b8663-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="b8663-165">toodo es así, de hello **archivo** menú en el Bloc de notas de hello, haga clic en **cerrar y detener la**.</span><span class="sxs-lookup"><span data-stu-id="b8663-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="b8663-166">Si tiene previsto toocomplete pasos de hello en un momento posterior, asegúrese de que eliminar el clúster de HDInsight de Hola que creó en este artículo.</span><span class="sxs-lookup"><span data-stu-id="b8663-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="b8663-167">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="b8663-167">Next step</span></span> 

<span data-ttu-id="b8663-168">En este artículo ha aprendido cómo toocreate una HDInsight Spark clúster y ejecutando un Spark SQL básicas de consulta.</span><span class="sxs-lookup"><span data-stu-id="b8663-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="b8663-169">Avanzar toohello siguiente artículo toolearn cómo toouse una HDInsight Spark clúster toorun realizar consultas interactivas en datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b8663-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b8663-170">Ejecución de consultas interactivas en un clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b8663-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



