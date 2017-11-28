---
title: "aaaMonitor clústeres de Hadoop en HDInsight utilizando Hola API Ambari - Azure | Documentos de Microsoft"
description: "Usar hello Apache Ambari APIs para crear, administrar y supervisar clústeres de Hadoop. API y las herramientas de operador intuitiva reducen la complejidad de Hola de Hadoop."
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
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="43194-104">Supervisar clústeres de Hadoop en HDInsight con Ambari API Hola</span><span class="sxs-lookup"><span data-stu-id="43194-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="43194-105">Obtenga información acerca de cómo toomonitor HDInsight clústeres utilizando Ambari APIs.</span><span class="sxs-lookup"><span data-stu-id="43194-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="43194-106">información de Hello en este artículo es principalmente para los clústeres de HDInsight basados en Windows, que proporciona una versión de solo lectura de hello API de REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="43194-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="43194-107">Para los clústeres basados en Linux, vea [Administrar clústeres de Hadoop mediante Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="43194-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="43194-108">¿Qué es Ambari?</span><span class="sxs-lookup"><span data-stu-id="43194-108">What is Ambari?</span></span>
<span data-ttu-id="43194-109">[Apache Ambari][ambari-home] sirve para el aprovisionamiento, la administración y la supervisión de clústeres de Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="43194-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="43194-110">Incluye una colección de herramientas de operador intuitiva y un potente conjunto de API que reducen la complejidad de Hola de Hadoop, simplificar la operación de Hola de clústeres.</span><span class="sxs-lookup"><span data-stu-id="43194-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="43194-111">Para obtener más información acerca de las API de hello, consulte [referencia de la API de Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="43194-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="43194-112">HDInsight admite actualmente solo hello Ambari característica de supervisión.</span><span class="sxs-lookup"><span data-stu-id="43194-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="43194-113">La API de Ambari v1.1.0 es compatible con los clústeres de las versiones 3.0 y 2.1 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43194-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="43194-114">Este artículo abarca el acceso a las API de Ambari en clústeres de las versiones 3.1 y 2.1 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43194-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="43194-115">Hola principal diferencia entre Hola dos es que algunos de los componentes de hello han cambiado con la introducción de Hola de nuevas capacidades (por ejemplo, Hola servidor del historial de trabajo).</span><span class="sxs-lookup"><span data-stu-id="43194-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="43194-116">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="43194-116">**Prerequisites**</span></span>

<span data-ttu-id="43194-117">Antes de comenzar este tutorial, debe tener Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="43194-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="43194-118">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="43194-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="43194-119">(Opcional) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="43194-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="43194-120">tooinstall, consulte [cURL versiones y descargas][curl-download].</span><span class="sxs-lookup"><span data-stu-id="43194-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="43194-121">Cuando usa el comando cURL de hello en Windows, utilice comillas dobles en lugar de comillas simples para los valores de opción de Hola.</span><span class="sxs-lookup"><span data-stu-id="43194-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="43194-122">**Un clúster de HDInsight de Azure**.</span><span class="sxs-lookup"><span data-stu-id="43194-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="43194-123">Para obtener instrucciones sobre el aprovisionamiento del clúster, consulte [Introducción al uso de HDInsight][hdinsight-get-started] o [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="43194-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="43194-124">Necesita Hola después toogo datos tutorial Hola:</span><span class="sxs-lookup"><span data-stu-id="43194-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="43194-125">Propiedad del clúster</span><span class="sxs-lookup"><span data-stu-id="43194-125">Cluster property</span></span> | <span data-ttu-id="43194-126">Nombre de variable de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="43194-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="43194-127">Valor</span><span class="sxs-lookup"><span data-stu-id="43194-127">Value</span></span> | <span data-ttu-id="43194-128">Description</span><span class="sxs-lookup"><span data-stu-id="43194-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="43194-129">Nombre del clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="43194-129">HDInsight cluster name</span></span> |<span data-ttu-id="43194-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="43194-130">$clusterName</span></span> | |<span data-ttu-id="43194-131">nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43194-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="43194-132">Nombre de usuario del clúster</span><span class="sxs-lookup"><span data-stu-id="43194-132">Cluster username</span></span> |<span data-ttu-id="43194-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="43194-133">$clusterUsername</span></span> | |<span data-ttu-id="43194-134">Nombre de usuario del clúster había especificado cuando se creó el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="43194-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="43194-135">Contraseña de clúster</span><span class="sxs-lookup"><span data-stu-id="43194-135">Cluster password</span></span> |<span data-ttu-id="43194-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="43194-136">$clusterPassword</span></span> | |<span data-ttu-id="43194-137">Contraseña de usuario de clúster</span><span class="sxs-lookup"><span data-stu-id="43194-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="43194-138">Jump-start</span><span class="sxs-lookup"><span data-stu-id="43194-138">Jump-start</span></span>
<span data-ttu-id="43194-139">Hay varias maneras de clústeres de HDInsight de toouse Ambari toomonitor.</span><span class="sxs-lookup"><span data-stu-id="43194-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="43194-140">**Uso de Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="43194-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="43194-141">Hola siguiente script de PowerShell de Azure obtiene información de seguimiento del trabajo de MapReduce de hello *en un clúster de HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="43194-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="43194-142">Hola principal diferencia es que se extracción estos detalles de servicio de hello YARN (en lugar de MapReduce).</span><span class="sxs-lookup"><span data-stu-id="43194-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="43194-143">Hola siguiente script de PowerShell obtiene información de seguimiento del trabajo de MapReduce de hello *en un clúster de HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="43194-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="43194-144">salida de Hello es:</span><span class="sxs-lookup"><span data-stu-id="43194-144">hello output is:</span></span>

![Salida de seguimiento de trabajo][img-jobtracker-output]

<span data-ttu-id="43194-146">**Uso de cURL**</span><span class="sxs-lookup"><span data-stu-id="43194-146">**Use cURL**</span></span>

<span data-ttu-id="43194-147">Hello en el ejemplo siguiente se obtiene información de clúster mediante cURL:</span><span class="sxs-lookup"><span data-stu-id="43194-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="43194-148">salida de Hello es:</span><span class="sxs-lookup"><span data-stu-id="43194-148">hello output is:</span></span>

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

<span data-ttu-id="43194-149">**Para la versión de Hola 10/8/2014**:</span><span class="sxs-lookup"><span data-stu-id="43194-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="43194-150">Al usar Hola Ambari punto de conexión, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}" hello *host_name* campo Devuelve el nombre de dominio completo (FQDN) de hello del nodo de hello en lugar del nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="43194-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="43194-151">Antes del lanzamiento de 10/8/2014 hello, este ejemplo devuelve simplemente "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="43194-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="43194-152">Después del lanzamiento de 10/8/2014 hello, obtendrá Hola FQDN "**headnode0. {} .Azurehdinsight ClusterDNS} .net**", como se muestra en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="43194-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="43194-153">Este cambio era escenarios toofacilitate requiere que se pueden implementar varios tipos de clúster (por ejemplo, HBase y Hadoop) en una red virtual (VNET).</span><span class="sxs-lookup"><span data-stu-id="43194-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="43194-154">Esto ocurre, por ejemplo, cuando se usa HBase como plataforma de back-end para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="43194-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="43194-155">API de supervisión de Ambari</span><span class="sxs-lookup"><span data-stu-id="43194-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="43194-156">Hello siguiente tabla enumeran algunas de hello más comunes Ambari supervisión llamadas API.</span><span class="sxs-lookup"><span data-stu-id="43194-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="43194-157">Para obtener más información acerca de la API de hello, consulte [referencia de la API de Ambari][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="43194-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="43194-158">Supervisión de la llamada a la API</span><span class="sxs-lookup"><span data-stu-id="43194-158">Monitor API call</span></span> | <span data-ttu-id="43194-159">URI</span><span class="sxs-lookup"><span data-stu-id="43194-159">URI</span></span> | <span data-ttu-id="43194-160">Description</span><span class="sxs-lookup"><span data-stu-id="43194-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43194-161">Obtener clústeres</span><span class="sxs-lookup"><span data-stu-id="43194-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="43194-162">Obtener información de clúster.</span><span class="sxs-lookup"><span data-stu-id="43194-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="43194-163">clústeres, servicios, hosts</span><span class="sxs-lookup"><span data-stu-id="43194-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="43194-164">Obtener servicios</span><span class="sxs-lookup"><span data-stu-id="43194-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="43194-165">Los servicios incluyen: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="43194-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="43194-166">Obtener información sobre los servicios.</span><span class="sxs-lookup"><span data-stu-id="43194-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="43194-167">Obtener componentes de servicio</span><span class="sxs-lookup"><span data-stu-id="43194-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="43194-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="43194-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="43194-169">Obtener información de componente.</span><span class="sxs-lookup"><span data-stu-id="43194-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="43194-170">ServiceComponentInfo, componentes de host, métricas</span><span class="sxs-lookup"><span data-stu-id="43194-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="43194-171">Obtener hosts</span><span class="sxs-lookup"><span data-stu-id="43194-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="43194-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="43194-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="43194-173">Obtener información sobre host.</span><span class="sxs-lookup"><span data-stu-id="43194-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="43194-174">Obtener componentes de host</span><span class="sxs-lookup"><span data-stu-id="43194-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="43194-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="43194-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="43194-176">Obtener información de componente de host</span><span class="sxs-lookup"><span data-stu-id="43194-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="43194-177">HostRoles, componente, host, métricas</span><span class="sxs-lookup"><span data-stu-id="43194-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="43194-178">Obtener configuraciones</span><span class="sxs-lookup"><span data-stu-id="43194-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="43194-179">Tipos de configuración: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="43194-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="43194-180">Obtener información de configuración</span><span class="sxs-lookup"><span data-stu-id="43194-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="43194-181">Tipos de configuración: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="43194-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43194-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43194-182">Next Steps</span></span>
<span data-ttu-id="43194-183">Ahora que ha aprendido cómo llama a toouse Ambari API de supervisión.</span><span class="sxs-lookup"><span data-stu-id="43194-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="43194-184">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="43194-184">toolearn more, see:</span></span>

* <span data-ttu-id="43194-185">[Administrar clústeres de HDInsight con hello portal de Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="43194-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="43194-186">[Administrar clústeres de HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="43194-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="43194-187">[Administrar clústeres de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="43194-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="43194-188">[Documentación de HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="43194-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="43194-189">[Introducción a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="43194-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
