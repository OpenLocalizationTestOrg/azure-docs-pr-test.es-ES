---
title: "Supervisión de clústeres de Hadoop en HDInsight con la API de Ambari (Azure) | Microsoft Docs"
description: "Use las API de Apache Ambari para crear, administrar y supervisar clústeres de Hadoop. Las API y herramientas de operador intuitivas ocultan la complejidad de Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="0a727-104">Supervisión de clústeres de Hadoop en HDInsight con la API de Ambari</span><span class="sxs-lookup"><span data-stu-id="0a727-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="0a727-105">Aprenda a supervisar clústeres de HDInsight con las API de Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a727-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="0a727-106">La información de este artículo es principalmente para los clústeres de HDInsight basados en Windows, que proporcionan una versión de solo lectura de la API de REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a727-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="0a727-107">Para los clústeres basados en Linux, vea [Administrar clústeres de Hadoop mediante Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="0a727-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="0a727-108">¿Qué es Ambari?</span><span class="sxs-lookup"><span data-stu-id="0a727-108">What is Ambari?</span></span>
<span data-ttu-id="0a727-109">[Apache Ambari][ambari-home] sirve para el aprovisionamiento, la administración y la supervisión de clústeres de Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0a727-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="0a727-110">Incluye una recopilación intuitiva de herramientas de operador y un conjunto sólido de API que ocultan la complejidad de Hadoop y simplifican la operación de clústeres.</span><span class="sxs-lookup"><span data-stu-id="0a727-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="0a727-111">Para obtener más información sobre las API, consulte [Referencia de API de Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="0a727-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="0a727-112">HDInsight actualmente solo es compatible con la característica de supervisión de Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a727-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="0a727-113">La API de Ambari v1.1.0 es compatible con los clústeres de las versiones 3.0 y 2.1 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a727-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="0a727-114">Este artículo abarca el acceso a las API de Ambari en clústeres de las versiones 3.1 y 2.1 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a727-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="0a727-115">La principal diferencia entre las dos es que algunos componentes han cambiado con la incorporación de nuevas funciones (como el servidor de historial de trabajos).</span><span class="sxs-lookup"><span data-stu-id="0a727-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="0a727-116">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="0a727-116">**Prerequisites**</span></span>

<span data-ttu-id="0a727-117">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a727-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="0a727-118">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0a727-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="0a727-119">(Opcional) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="0a727-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="0a727-120">Para instalarlo, consulte [Descargas y versiones de cURL][curl-download].</span><span class="sxs-lookup"><span data-stu-id="0a727-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0a727-121">Cuando utilice el comando cURL en Windows, utilice comillas dobles en lugar de comillas simples para los valores de opción.</span><span class="sxs-lookup"><span data-stu-id="0a727-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="0a727-122">**Un clúster de HDInsight de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0a727-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="0a727-123">Para obtener instrucciones sobre el aprovisionamiento del clúster, consulte [Introducción al uso de HDInsight][hdinsight-get-started] o [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="0a727-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="0a727-124">Para completar el tutorial, necesita los datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0a727-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="0a727-125">Propiedad del clúster</span><span class="sxs-lookup"><span data-stu-id="0a727-125">Cluster property</span></span> | <span data-ttu-id="0a727-126">Nombre de variable de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a727-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="0a727-127">Valor</span><span class="sxs-lookup"><span data-stu-id="0a727-127">Value</span></span> | <span data-ttu-id="0a727-128">Description</span><span class="sxs-lookup"><span data-stu-id="0a727-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="0a727-129">Nombre del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a727-129">HDInsight cluster name</span></span> |<span data-ttu-id="0a727-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="0a727-130">$clusterName</span></span> | |<span data-ttu-id="0a727-131">El nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a727-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="0a727-132">Nombre de usuario del clúster</span><span class="sxs-lookup"><span data-stu-id="0a727-132">Cluster username</span></span> |<span data-ttu-id="0a727-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="0a727-133">$clusterUsername</span></span> | |<span data-ttu-id="0a727-134">Nombre de usuario del clúster especificado cuando se creó el clúster.</span><span class="sxs-lookup"><span data-stu-id="0a727-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="0a727-135">Contraseña de clúster</span><span class="sxs-lookup"><span data-stu-id="0a727-135">Cluster password</span></span> |<span data-ttu-id="0a727-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="0a727-136">$clusterPassword</span></span> | |<span data-ttu-id="0a727-137">Contraseña de usuario de clúster</span><span class="sxs-lookup"><span data-stu-id="0a727-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="0a727-138">Jump-start</span><span class="sxs-lookup"><span data-stu-id="0a727-138">Jump-start</span></span>
<span data-ttu-id="0a727-139">Existen varias maneras de usar Ambari para supervisar clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a727-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="0a727-140">**Uso de Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0a727-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="0a727-141">El siguiente es un script de Azure PowerShell para obtener la información del seguimiento de trabajos de MapReduce *en un clúster de HDInsight 3.5*.</span><span class="sxs-lookup"><span data-stu-id="0a727-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="0a727-142">La principal diferencia aquí es que extraemos estos detalles del servicio YARN (en lugar de MapReduce).</span><span class="sxs-lookup"><span data-stu-id="0a727-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="0a727-143">El siguiente es un script de PowerShell para obtener la información del seguimiento de trabajos de MapReduce *en un clúster de HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="0a727-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="0a727-144">El salida es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a727-144">The output is:</span></span>

![Salida de seguimiento de trabajo][img-jobtracker-output]

<span data-ttu-id="0a727-146">**Uso de cURL**</span><span class="sxs-lookup"><span data-stu-id="0a727-146">**Use cURL**</span></span>

<span data-ttu-id="0a727-147">En el ejemplo siguiente se obtiene información de clúster mediante el uso de cURL:</span><span class="sxs-lookup"><span data-stu-id="0a727-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="0a727-148">El salida es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a727-148">The output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="0a727-149">**Para la versión del 10/8/2014**:</span><span class="sxs-lookup"><span data-stu-id="0a727-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="0a727-150">Cuando se usa el extremo Ambari, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", el campo *host_name* devuelve ahora el nombre de dominio completo (FQDN) del nodo en lugar de solo el nombre del host.</span><span class="sxs-lookup"><span data-stu-id="0a727-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="0a727-151">Antes de la versión del 8/10/2014, este ejemplo devolvía simplemente "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="0a727-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="0a727-152">Después de la versión del 8/10/2014, se obtiene el FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", como se muestra en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="0a727-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="0a727-153">Este cambio se solicitó para facilitar escenarios donde se pueden implementar varios tipos de clúster (como HBase y Hadoop) en una misma red virtual (VNET).</span><span class="sxs-lookup"><span data-stu-id="0a727-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="0a727-154">Esto ocurre, por ejemplo, cuando se usa HBase como plataforma de back-end para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0a727-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="0a727-155">API de supervisión de Ambari</span><span class="sxs-lookup"><span data-stu-id="0a727-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="0a727-156">En la siguiente lista se enumeran algunas de las llamadas a API desde la supervisión de Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a727-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="0a727-157">Para obtener más información sobre la API, consulte [Referencia de API de Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="0a727-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="0a727-158">Supervisión de la llamada a la API</span><span class="sxs-lookup"><span data-stu-id="0a727-158">Monitor API call</span></span> | <span data-ttu-id="0a727-159">URI</span><span class="sxs-lookup"><span data-stu-id="0a727-159">URI</span></span> | <span data-ttu-id="0a727-160">Description</span><span class="sxs-lookup"><span data-stu-id="0a727-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0a727-161">Obtener clústeres</span><span class="sxs-lookup"><span data-stu-id="0a727-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="0a727-162">Obtener información de clúster.</span><span class="sxs-lookup"><span data-stu-id="0a727-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="0a727-163">clústeres, servicios, hosts</span><span class="sxs-lookup"><span data-stu-id="0a727-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="0a727-164">Obtener servicios</span><span class="sxs-lookup"><span data-stu-id="0a727-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="0a727-165">Los servicios incluyen: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="0a727-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="0a727-166">Obtener información sobre los servicios.</span><span class="sxs-lookup"><span data-stu-id="0a727-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="0a727-167">Obtener componentes de servicio</span><span class="sxs-lookup"><span data-stu-id="0a727-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="0a727-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="0a727-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="0a727-169">Obtener información de componente.</span><span class="sxs-lookup"><span data-stu-id="0a727-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="0a727-170">ServiceComponentInfo, componentes de host, métricas</span><span class="sxs-lookup"><span data-stu-id="0a727-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="0a727-171">Obtener hosts</span><span class="sxs-lookup"><span data-stu-id="0a727-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="0a727-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="0a727-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="0a727-173">Obtener información sobre host.</span><span class="sxs-lookup"><span data-stu-id="0a727-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="0a727-174">Obtener componentes de host</span><span class="sxs-lookup"><span data-stu-id="0a727-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="0a727-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="0a727-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="0a727-176">Obtener información de componente de host</span><span class="sxs-lookup"><span data-stu-id="0a727-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="0a727-177">HostRoles, componente, host, métricas</span><span class="sxs-lookup"><span data-stu-id="0a727-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="0a727-178">Obtener configuraciones</span><span class="sxs-lookup"><span data-stu-id="0a727-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="0a727-179">Tipos de configuración: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="0a727-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="0a727-180">Obtener información de configuración</span><span class="sxs-lookup"><span data-stu-id="0a727-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="0a727-181">Tipos de configuración: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="0a727-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a727-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a727-182">Next Steps</span></span>
<span data-ttu-id="0a727-183">Ahora sabe cómo usar las llamadas de API de supervisión de Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a727-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="0a727-184">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="0a727-184">To learn more, see:</span></span>

* <span data-ttu-id="0a727-185">[Administrar clústeres de HDInsight con Azure Portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="0a727-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="0a727-186">[Administrar clústeres de HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="0a727-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="0a727-187">[Administrar clústeres de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="0a727-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="0a727-188">[Documentación de HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="0a727-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="0a727-189">[Introducción a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0a727-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
