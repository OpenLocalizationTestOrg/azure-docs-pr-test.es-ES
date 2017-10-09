---
title: "aaaApache Spark estructurado de transmisión por secuencias con Kafka - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Apache Spark transmisión por secuencias (DStream) tooget datos entre o salga de Apache Kafka. En este ejemplo, se transmiten datos con Jupyter Notebook de Spark en HDInsight."
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
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="c9c72-104">Uso del flujo estructurado de Spark con Kafka (versión preliminar) en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9c72-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="c9c72-105">Obtenga información acerca de cómo toouse Spark estructurado de transmisión por secuencias de datos de tooread de Kafka de Apache en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c72-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="c9c72-106">El flujo estructurado de Spark es un motor de procesamiento de flujo basado en Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="c9c72-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="c9c72-107">Permite que los cálculos de transmisión por secuencias de tooexpress Hola igual que el cálculo de lote de datos estáticos.</span><span class="sxs-lookup"><span data-stu-id="c9c72-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="c9c72-108">Para obtener más información sobre estructurado de transmisión por secuencias, vea hello [estructurado Streaming Guía de programación [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) en Apache.org.</span><span class="sxs-lookup"><span data-stu-id="c9c72-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9c72-109">En este ejemplo se utiliza Spark 2.1 en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="c9c72-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="c9c72-110">La versión de la funcionalidad de flujo estructurado se considera __alfa__ en Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="c9c72-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="c9c72-111">pasos de Hello en este documento crea un grupo de recursos de Azure que contiene tanto un Spark en HDInsight y un Kafka en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9c72-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="c9c72-112">Estos clústeres son ambos ubicados en una red Virtual de Azure, lo que permite hello toodirectly de clúster de Spark comunican con hello clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="c9c72-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="c9c72-113">Cuando haya terminado con pasos de hello en este documento, recuerde toodelete Hola clústeres tooavoid exceso cargos.</span><span class="sxs-lookup"><span data-stu-id="c9c72-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="c9c72-114">Crear clústeres de Hola</span><span class="sxs-lookup"><span data-stu-id="c9c72-114">Create hello clusters</span></span>

<span data-ttu-id="c9c72-115">Apache Kafka en HDInsight no ofrece acceso toohello Kafka corredores de bolsa respecto Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="c9c72-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="c9c72-116">Todo lo que tooKafka debe estar en las conversaciones Hola misma red virtual de Azure como nodos de hello en Hola clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="c9c72-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="c9c72-117">En este ejemplo, hello Kafka y clústeres de Spark se encuentran en una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c72-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="c9c72-118">Hello diagrama siguiente muestra cómo fluye la comunicación entre clústeres de hello:</span><span class="sxs-lookup"><span data-stu-id="c9c72-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clústeres Spark y Kafka en una red virtual de Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="c9c72-120">Hola servicio Kafka es limitado toocommunication dentro de la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="c9c72-121">Otros servicios en clúster de hello, como SSH y Ambari, puede tener acceso a través de Hola a internet.</span><span class="sxs-lookup"><span data-stu-id="c9c72-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="c9c72-122">Para obtener más información sobre los puertos públicos de hello disponibles con HDInsight, vea [puertos y URI utilizado por HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="c9c72-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="c9c72-123">Si bien puede crear una red virtual de Azure, Kafka y Spark clústeres manualmente, resulta más fácil toouse una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9c72-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="c9c72-124">Use Hola siguientes pasos le indican una red virtual de Azure, Kafka, toodeploy y Spark clústeres tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c72-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="c9c72-125">Usar hello siguientes toosign de botón en tooAzure y plantilla abierto Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c72-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="c9c72-126">Hello plantilla de Azure Resource Manager se encuentra en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="c9c72-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="c9c72-127">Esta plantilla crea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9c72-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="c9c72-128">Un clúster de Kafka en HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="c9c72-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="c9c72-129">Un clúster de Spark en HDInsight 3.6</span><span class="sxs-lookup"><span data-stu-id="c9c72-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="c9c72-130">Una red Virtual de Azure, que contiene los clústeres de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c9c72-131">Hola estructurado streaming Bloc de notas utilizado en este ejemplo requiere Spark en HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="c9c72-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="c9c72-132">Si usa una versión anterior de Spark en HDInsight, recibirá errores al usar el Bloc de notas de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="c9c72-133">Hola uso seguidas de hello las entradas de información toopopulate hello **implementación personalizada** hoja:</span><span class="sxs-lookup"><span data-stu-id="c9c72-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Implementación personalizada de HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="c9c72-135">**Grupo de recursos**: cree un nuevo grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="c9c72-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="c9c72-136">Este grupo contiene clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="c9c72-137">**Ubicación**: seleccione una tooyou geográficamente cerrar de ubicación.</span><span class="sxs-lookup"><span data-stu-id="c9c72-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="c9c72-138">**Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="c9c72-139">Por ejemplo, si especifica **hdi**, creará un clúster Spark denominado spark-hdi__ y un clúster Kafka denominado **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="c9c72-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="c9c72-140">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario de administrador de Hola para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c9c72-141">**Contraseña de inicio de sesión del clúster**: contraseña de usuario de administrador de Hola para clústeres de Spark y Kafka de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c9c72-142">**Nombre de usuario SSH**: Hola toocreate de usuario SSH para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c9c72-143">**Contraseña SSH**: contraseña de hello para el usuario SSH de Hola para clústeres de Spark y Kafka Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="c9c72-144">Hola de lectura **términos y condiciones**y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="c9c72-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="c9c72-145">Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**.</span><span class="sxs-lookup"><span data-stu-id="c9c72-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="c9c72-146">Tarda aproximadamente 20 minutos toocreate clústeres Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="c9c72-147">Una vez que se han creado los recursos de hello, son hoja del grupo de recursos de toohello redirigida.</span><span class="sxs-lookup"><span data-stu-id="c9c72-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Hoja de grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="c9c72-149">Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME spark** y **kafka BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="c9c72-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="c9c72-150">Utilice estos nombres en pasos posteriores al conectarse a clústeres de toohello.</span><span class="sxs-lookup"><span data-stu-id="c9c72-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="c9c72-151">Obtener hello Kafka corredores de bolsa</span><span class="sxs-lookup"><span data-stu-id="c9c72-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="c9c72-152">código de este ejemplo Hello conecta toohello Kafka hosts en clúster Kafka Hola de broker.</span><span class="sxs-lookup"><span data-stu-id="c9c72-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="c9c72-153">toofind Hola hosts de broker Kafka, usar hello PowerShell o Bash ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9c72-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
> <span data-ttu-id="c9c72-154">En este ejemplo espera `$PASSWORD` toocontain contraseña de Hola para inicio de sesión de clúster de hello, y `$CLUSTERNAME` toocontain nombre de Hola de hello clúster Kafka.</span><span class="sxs-lookup"><span data-stu-id="c9c72-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="c9c72-155">Este ejemplo utiliza hello [jq](https://stedolan.github.io/jq/) datos de utilidad tooparse fuera del documento JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="c9c72-156">Hola de salida es toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="c9c72-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="c9c72-157">Guarde esta información, tal como se utiliza en hello siguientes secciones de este documento.</span><span class="sxs-lookup"><span data-stu-id="c9c72-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="c9c72-158">Obtener los blocs de notas de Hola</span><span class="sxs-lookup"><span data-stu-id="c9c72-158">Get hello notebooks</span></span>

<span data-ttu-id="c9c72-159">código de Hello de ejemplo de Hola descrita en este documento está disponible en [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="c9c72-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="c9c72-160">Cargar blocs de notas de Hola</span><span class="sxs-lookup"><span data-stu-id="c9c72-160">Upload hello notebooks</span></span>

<span data-ttu-id="c9c72-161">Usar hello siguiendo los pasos tooupload Hola blocs de notas de hello proyecto tooyour Spark en clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c9c72-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="c9c72-162">En el explorador web, conéctese toohello Jupyter notebook en su clúster Spark.</span><span class="sxs-lookup"><span data-stu-id="c9c72-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="c9c72-163">Hola después de la dirección URL, reemplace `CLUSTERNAME` con el nombre de hello del clúster Kafka:</span><span class="sxs-lookup"><span data-stu-id="c9c72-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="c9c72-164">Cuando se le solicite, escriba inicio de sesión de clúster de hello (admin) y la contraseña que utilizó cuando creó el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="c9c72-165">Desde Hola superior derecha de la página de hello, use hello __cargar__ Hola de botón tooupload __secuencia-Tweets-To_Kafka.ipynb__ clúster toohello de archivos.</span><span class="sxs-lookup"><span data-stu-id="c9c72-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="c9c72-166">Seleccione __abiertos__ carga de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="c9c72-166">Select __Open__ toostart hello upload.</span></span>

    ![Usar Hola carga botón tooselect y cargar un bloc de notas](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Seleccione el archivo de hello KafkaStreaming.ipynb](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="c9c72-169">Buscar hello __secuencia-Tweets-To_Kafka.ipynb__ entrada de lista de Hola de blocs de notas y seleccione __cargar__ junto a él.</span><span class="sxs-lookup"><span data-stu-id="c9c72-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Carga de uso Hola situado junto a la tooupload de entrada de hello KafkaStreaming.ipynb se toohello servidor de Bloc de notas](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="c9c72-171">Repita los pasos Hola de 1 a 3 tooload __Spark-estructura-Streaming-de-Kafka.ipynb__ Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="c9c72-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="c9c72-172">Carga de tweets en Kafka</span><span class="sxs-lookup"><span data-stu-id="c9c72-172">Load tweets into Kafka</span></span>

<span data-ttu-id="c9c72-173">Una vez que se han cargado los archivos de hello, seleccione hello __secuencia-Tweets-To_Kafka.ipynb__ Bloc de notas de entrada tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c72-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="c9c72-174">Siga los pasos Hola Hola Bloc de notas tooload tweets en Kafka.</span><span class="sxs-lookup"><span data-stu-id="c9c72-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="c9c72-175">Procesamiento de tweets mediante el flujo estructurado de Spark</span><span class="sxs-lookup"><span data-stu-id="c9c72-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="c9c72-176">En página principal de Jupyter Notebook hello, seleccione hello __Spark-estructura-Streaming-de-Kafka.ipynb__ entrada.</span><span class="sxs-lookup"><span data-stu-id="c9c72-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="c9c72-177">Siga los pasos Hola Hola Bloc de notas tooload tweets desde Kafka mediante transmisión por secuencias estructurado Spark.</span><span class="sxs-lookup"><span data-stu-id="c9c72-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c72-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9c72-178">Next steps</span></span>

<span data-ttu-id="c9c72-179">Ahora que ha aprendido cómo toouse Spark estructurado transmisión por secuencias, vea Hola después toolearn documentos más sobre cómo trabajar con Spark y Kafka:</span><span class="sxs-lookup"><span data-stu-id="c9c72-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="c9c72-180">[¿Cómo toouse inspirará transmisión por secuencias (DStream) con Kafka](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="c9c72-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="c9c72-181">Introducción a Jupyter Notebook y Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9c72-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)