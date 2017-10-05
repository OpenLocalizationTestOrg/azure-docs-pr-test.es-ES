---
title: 'Flujo estructurado de Apache Spark con Kafka: Azure HDInsight | Microsoft Docs'
description: Aprenda a usar el streaming de Apache Spark (DStream) para obtener datos dentro o fuera de Apache Kafka. En este ejemplo, se transmiten datos con Jupyter Notebook de Spark en HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="e4e84-104">Uso del flujo estructurado de Spark con Kafka (versión preliminar) en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4e84-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="e4e84-105">Obtenga información sobre cómo usar el flujo estructurado de Spark para leer datos de Apache Kafka en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4e84-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="e4e84-106">El flujo estructurado de Spark es un motor de procesamiento de flujo basado en Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="e4e84-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="e4e84-107">Permite expresar los cálculos de streaming de la misma forma que el cálculo por lotes de los datos estáticos.</span><span class="sxs-lookup"><span data-stu-id="e4e84-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="e4e84-108">Para obtener más información sobre el flujo estructurado, consulte el artículo [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) (Guía de programación de flujo estructurado [alfa]) en Apache.org.</span><span class="sxs-lookup"><span data-stu-id="e4e84-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4e84-109">En este ejemplo se utiliza Spark 2.1 en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e4e84-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="e4e84-110">La versión de la funcionalidad de flujo estructurado se considera __alfa__ en Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="e4e84-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="e4e84-111">Los pasos que se describen en este documento crean un grupo de recursos de Azure que contiene un clúster Spark de HDInsight y un clúster Kafka de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4e84-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="e4e84-112">Estos dos clústeres se encuentran en una red virtual de Azure, lo que permite al clúster Spark comunicarse directamente con el clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="e4e84-113">Cuando haya terminado los pasos indicados en este documento, no olvide eliminar los clústeres para evitar gastos innecesarios.</span><span class="sxs-lookup"><span data-stu-id="e4e84-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="e4e84-114">Creación de los clústeres</span><span class="sxs-lookup"><span data-stu-id="e4e84-114">Create the clusters</span></span>

<span data-ttu-id="e4e84-115">Apache Kafka en HDInsight no proporciona acceso a los agentes de Kafka a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="e4e84-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="e4e84-116">Cualquier comunicación con Kafka debe realizarse en la misma red virtual de Azure que utilizan los nodos del clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="e4e84-117">En este ejemplo, los clústeres Kafka y Spark se encuentran en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4e84-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="e4e84-118">En el diagrama siguiente, se muestra cómo fluye la comunicación entre los clústeres:</span><span class="sxs-lookup"><span data-stu-id="e4e84-118">The following diagram shows how communication flows between the clusters:</span></span>

![Diagrama de clústeres Spark y Kafka en una red virtual de Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="e4e84-120">El servicio Kafka se limita a la comunicación dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="e4e84-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="e4e84-121">Se puede acceder a otros servicios del clúster, como SSH y Ambari, a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="e4e84-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="e4e84-122">Para más información sobre los puertos públicos disponibles en HDInsight, consulte [Puertos e identificadores URI usados en HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e4e84-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="e4e84-123">Aunque puede crear manualmente la red virtual de Azure y los clústeres Kafka y Spark, resulta más sencillo utilizar una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e4e84-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="e4e84-124">Siga los pasos que se indican a continuación para implementar una red virtual de Azure y los clústeres Kafka y Spark en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4e84-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="e4e84-125">Utilice el siguiente botón para iniciar sesión en Azure y abrir la plantilla en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4e84-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="e4e84-126">La plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="e4e84-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="e4e84-127">Esta plantilla crea los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="e4e84-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="e4e84-128">Un clúster de Kafka en HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="e4e84-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="e4e84-129">Un clúster de Spark en HDInsight 3.6</span><span class="sxs-lookup"><span data-stu-id="e4e84-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="e4e84-130">Una red virtual de Azure, que contiene los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4e84-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e4e84-131">El cuaderno de flujo estructurado que se utiliza en este ejemplo requiere Spark en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="e4e84-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="e4e84-132">Si usa una versión anterior de Spark en HDInsight, recibirá errores al usar dicho cuaderno.</span><span class="sxs-lookup"><span data-stu-id="e4e84-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="e4e84-133">Utilice los datos siguientes para rellenar las entradas de la hoja **Implementación personalizada**:</span><span class="sxs-lookup"><span data-stu-id="e4e84-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="e4e84-135">**Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="e4e84-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="e4e84-136">Este grupo contiene el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e4e84-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="e4e84-137">**Ubicación**: seleccione una ubicación geográfica próxima a usted.</span><span class="sxs-lookup"><span data-stu-id="e4e84-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="e4e84-138">**Base Cluster Name** (Nombre base del clúster): este valor se utiliza como nombre base en los clústeres Spark y Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="e4e84-139">Por ejemplo, si especifica **hdi**, creará un clúster Spark denominado spark-hdi__ y un clúster Kafka denominado **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="e4e84-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="e4e84-140">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario del administrador de los clústeres Spark y Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e4e84-141">**Contraseña de inicio de sesión de clúster**: contraseña del usuario administrador para los clústeres Spark y Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e4e84-142">**Nombre de usuario SSH**: usuario de SSH que se va a crear para los clústeres Spark y Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="e4e84-143">**Contraseña SSH**: contraseña del usuario de SSH para los clústeres Spark y Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="e4e84-144">Consulte los **Términos y condiciones** y seleccione **Acepto los términos y condiciones indicados anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="e4e84-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="e4e84-145">Por último, active **Anclar al panel** y seleccione **Adquirir**.</span><span class="sxs-lookup"><span data-stu-id="e4e84-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="e4e84-146">Se tarda aproximadamente 20 minutos en crear los clústeres.</span><span class="sxs-lookup"><span data-stu-id="e4e84-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="e4e84-147">Cuando se hayan creado los recursos, se le redirigirá a la hoja de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e4e84-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![Hoja de grupo de recursos de la red virtual y clústeres](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="e4e84-149">Observe que los nombres de los clústeres de HDInsight son **spark-BASENAME** y **kafka-BASENAME**, donde BASENAME es el nombre que indicó en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e4e84-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="e4e84-150">Estos nombres se utilizarán más adelante al establecer la conexión con los clústeres.</span><span class="sxs-lookup"><span data-stu-id="e4e84-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="e4e84-151">Obtención de los agentes de Kafka</span><span class="sxs-lookup"><span data-stu-id="e4e84-151">Get the Kafka brokers</span></span>

<span data-ttu-id="e4e84-152">El código de este ejemplo se conecta a los hosts de los agentes de Kafka del clúster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="e4e84-153">Para buscar los hosts de los agentes de Kafka, use el siguiente ejemplo de PowerShell o Bash:</span><span class="sxs-lookup"><span data-stu-id="e4e84-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="e4e84-154">En este ejemplo se espera que `$PASSWORD` contenga la contraseña del inicio de sesión del clúster, y que `$CLUSTERNAME` incluya el nombre del clúster de Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="e4e84-155">En este ejemplo se utiliza la utilidad [jq](https://stedolan.github.io/jq/) para analizar datos a partir del documento JSON.</span><span class="sxs-lookup"><span data-stu-id="e4e84-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="e4e84-156">La salida será similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e4e84-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="e4e84-157">Guarde esta información, ya que se utilizará en las siguientes secciones de este documento.</span><span class="sxs-lookup"><span data-stu-id="e4e84-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="e4e84-158">Obtención de los cuadernos</span><span class="sxs-lookup"><span data-stu-id="e4e84-158">Get the notebooks</span></span>

<span data-ttu-id="e4e84-159">El código del ejemplo que se describe en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="e4e84-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="e4e84-160">Carga de los cuadernos</span><span class="sxs-lookup"><span data-stu-id="e4e84-160">Upload the notebooks</span></span>

<span data-ttu-id="e4e84-161">Siga estos pasos para cargar los cuadernos del proyecto en el clúster de Spark en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e4e84-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="e4e84-162">En el explorador web, conéctese al cuaderno de Jupyter Notebook en el clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="e4e84-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="e4e84-163">En la siguiente URL, reemplace `CLUSTERNAME` por el nombre del clúster de Kafka:</span><span class="sxs-lookup"><span data-stu-id="e4e84-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="e4e84-164">Cuando se lo soliciten, escriba el nombre de inicio de sesión del clúster (administrador) y la contraseña que utilizó cuando creó el clúster.</span><span class="sxs-lookup"><span data-stu-id="e4e84-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="e4e84-165">En la parte superior derecha de la página, utilice el botón __Upload__ (Cargar) para cargar el archivo __Stream-Tweets-To_Kafka.ipynb__ en el clúster.</span><span class="sxs-lookup"><span data-stu-id="e4e84-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="e4e84-166">Seleccione __Open__ (Abrir) para iniciar la carga.</span><span class="sxs-lookup"><span data-stu-id="e4e84-166">Select __Open__ to start the upload.</span></span>

    ![Para seleccionar y cargar un cuaderno, utilice el botón de carga.](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Seleccione el archivo KafkaStreaming.ipynb.](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="e4e84-169">Busque la entrada __Stream-Tweets-To_Kafka.ipynb__ en la lista de cuadernos y seleccione el botón __Upload__ (Cargar) que está junto a ella.</span><span class="sxs-lookup"><span data-stu-id="e4e84-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Utilice el botón Upload (Cargar) que está situado junto a la entrada KafkaStreaming.ipynb para cargar el archivo en el servidor de cuadernos.](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="e4e84-171">Repita los pasos del 1 a 3 para cargar el cuaderno __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="e4e84-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="e4e84-172">Carga de tweets en Kafka</span><span class="sxs-lookup"><span data-stu-id="e4e84-172">Load tweets into Kafka</span></span>

<span data-ttu-id="e4e84-173">Cuando se hayan cargado los archivos, seleccione la entrada __Stream-Tweets-To_Kafka.ipynb__ para abrir el cuaderno.</span><span class="sxs-lookup"><span data-stu-id="e4e84-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="e4e84-174">Siga los pasos descritos en el cuaderno para cargar tweets en Kafka.</span><span class="sxs-lookup"><span data-stu-id="e4e84-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="e4e84-175">Procesamiento de tweets mediante el flujo estructurado de Spark</span><span class="sxs-lookup"><span data-stu-id="e4e84-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="e4e84-176">En la página principal de Jupyter Notebook, seleccione la entrada __Spark-Structured-Streaming-From-Kafka.ipynb__.</span><span class="sxs-lookup"><span data-stu-id="e4e84-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="e4e84-177">Siga los pasos descritos en el cuaderno para cargar tweets de Kafka mediante el flujo estructurado de Spark.</span><span class="sxs-lookup"><span data-stu-id="e4e84-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4e84-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4e84-178">Next steps</span></span>

<span data-ttu-id="e4e84-179">Ahora que ha aprendido a usar el flujo estructurado de Spark, consulte los siguientes documentos para obtener más información sobre cómo trabajar con Spark y Kafka:</span><span class="sxs-lookup"><span data-stu-id="e4e84-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="e4e84-180">[Uso del flujo estructurado de Spark (DStream) con Kafka](hdinsight-apache-spark-with-kafka.md)</span><span class="sxs-lookup"><span data-stu-id="e4e84-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="e4e84-181">Introducción a Jupyter Notebook y Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e4e84-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)