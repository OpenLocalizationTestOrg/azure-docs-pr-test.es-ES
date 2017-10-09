---
title: aaaMonitor y administrar Hadoop con la API de REST de Ambari - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Ambari toomonitor y administrar clústeres de Hadoop en HDInsight de Azure. En este documento, obtendrá información sobre cómo clústeres toouse Hola API de REST de Ambari incluido con HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="44327-104">Administrar clústeres de HDInsight con Ambari API de REST de Hola</span><span class="sxs-lookup"><span data-stu-id="44327-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="44327-105">Obtenga información acerca de cómo toouse Hola API de REST de Ambari toomanage y supervisar clústeres de Hadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="44327-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="44327-106">Apache Ambari simplifica la administración de Hola y supervisión de un clúster de Hadoop proporcionando fácil toouse web API de REST y de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="44327-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="44327-107">Ambari se incluye en los clústeres de HDInsight que usan el sistema operativo de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="44327-108">Puede usar Ambari toomonitor Hola clúster y realizar cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="44327-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="44327-109"><a id="whatis"></a>¿Qué es Ambari?</span><span class="sxs-lookup"><span data-stu-id="44327-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="44327-110">[Apache Ambari](http://ambari.apache.org) proporciona la interfaz de usuario que puede ser usado tooprovision, administrar y supervisar clústeres de Hadoop web.</span><span class="sxs-lookup"><span data-stu-id="44327-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="44327-111">Los desarrolladores pueden integrar estas capacidades en sus aplicaciones mediante el uso de hello [API de REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="44327-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="44327-112">De manera predeterminada, Ambari viene con los clústeres de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="44327-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="44327-113">¿Cómo toouse Hola Ambari API de REST</span><span class="sxs-lookup"><span data-stu-id="44327-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44327-114">Hola información y ejemplos de este documento requieren un clúster de HDInsight que usa el sistema operativo Linux.</span><span class="sxs-lookup"><span data-stu-id="44327-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="44327-115">Para más información, vea la [introducción a HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44327-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="44327-116">ejemplos de Hello en este documento se proporcionan para que el shell de Bourne hello (intensiva de errores) y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44327-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="44327-117">bash Hola ejemplos se han probado con GNU bash 4.3.11, pero deben funcionar con otros shells de Unix.</span><span class="sxs-lookup"><span data-stu-id="44327-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="44327-118">ejemplos de PowerShell de Hola se han probado con PowerShell 5.0, pero deberían funcionar con PowerShell 3.0 o superior.</span><span class="sxs-lookup"><span data-stu-id="44327-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="44327-119">Si usa hello __shell Bourne__ (intensiva de errores), debe tener instalado el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="44327-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="44327-120">[cURL](http://curl.haxx.se/): cURL es una utilidad que puede ser toowork utilizado con las API de REST de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="44327-121">En este documento, es toocommunicate usado con hello API de REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="44327-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="44327-122">Tanto si usa Bash como PowerShell, también debe tener [jq](https://stedolan.github.io/jq/) instalado.</span><span class="sxs-lookup"><span data-stu-id="44327-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="44327-123">Jq es una utilidad para trabajar con documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="44327-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="44327-124">Se utiliza en **todos los** Hola ejemplos intensiva de errores, y **una** de ejemplos de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="44327-125">URI base para la API de REST de Ambari</span><span class="sxs-lookup"><span data-stu-id="44327-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="44327-126">URI base para hello API de REST de Ambari en HDInsight Hello es https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, donde **CLUSTERNAME** es Hola nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="44327-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44327-127">Mientras el nombre de clúster de Hola Hola completo parte del dominio (FQDN) del nombre del programa Hola URI (CLUSTERNAME.azurehdinsight.net) distingue mayúsculas de minúsculas, otras apariciones en hello URI distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="44327-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="44327-128">Por ejemplo, si el clúster se denomina `MyCluster`, siguiente Hola es URI válidos:</span><span class="sxs-lookup"><span data-stu-id="44327-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="44327-129">siguiente Hola URI devuelve un error porque no es Hola Hola segunda aparición del nombre de hello corregir caso.</span><span class="sxs-lookup"><span data-stu-id="44327-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="44327-130">Autenticación</span><span class="sxs-lookup"><span data-stu-id="44327-130">Authentication</span></span>

<span data-ttu-id="44327-131">Conexión tooAmbari en HDInsight requiere HTTPS.</span><span class="sxs-lookup"><span data-stu-id="44327-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="44327-132">Nombre de la cuenta de administrador de uso hello (valor predeterminado de hello es **administración**) y la contraseña proporcionados durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="44327-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="44327-133">Ejemplos: Autenticación y análisis JSON</span><span class="sxs-lookup"><span data-stu-id="44327-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="44327-134">Hello en los ejemplos siguientes muestra cómo toomake una solicitud GET en hello base Ambari API de REST:</span><span class="sxs-lookup"><span data-stu-id="44327-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="44327-135">en los ejemplos de este documento Hola intensiva de errores que Hola siguientes supuestos:</span><span class="sxs-lookup"><span data-stu-id="44327-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="44327-136">nombre de inicio de sesión de Hello para el clúster de hello es Hola valor predeterminado `admin`.</span><span class="sxs-lookup"><span data-stu-id="44327-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="44327-137">`$PASSWORD`contiene la contraseña de Hola para hello comando de inicio de sesión de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44327-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="44327-138">Puede establecer este valor mediante `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="44327-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="44327-139">`$CLUSTERNAME`contiene el nombre de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="44327-140">Puede establecer este valor mediante `set CLUSTERNAME='clustername'`.</span><span class="sxs-lookup"><span data-stu-id="44327-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="44327-141">ejemplos de PowerShell de Hello en este documento que Hola siguientes supuestos:</span><span class="sxs-lookup"><span data-stu-id="44327-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="44327-142">`$creds`es un objeto de credencial que contiene el inicio de sesión de administrador de hello y una contraseña para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="44327-143">Puede establecer este valor mediante `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` y proporcionar las credenciales de hello cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="44327-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="44327-144">`$clusterName`es una cadena que contiene el nombre de hello del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="44327-145">Puede establecer este valor mediante `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="44327-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="44327-146">Ambos ejemplos devuelven un documento JSON que comienza con información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44327-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a><span data-ttu-id="44327-147">Análisis de datos JSON</span><span class="sxs-lookup"><span data-stu-id="44327-147">Parsing JSON data</span></span>

<span data-ttu-id="44327-148">Hello siguiente ejemplo se utiliza `jq` tooparse Hola documento de respuesta JSON y mostrar solo hello `health_report` información de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="44327-149">PowerShell 3.0 y versiones posterior proporciona hello `ConvertFrom-Json` cmdlet, que convierte el documento JSON de hello en un objeto que es más fácil toowork con de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44327-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="44327-150">Hello siguiente ejemplo se utiliza `ConvertFrom-Json` toodisplay solo hello `health_report` información de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="44327-151">Aunque la mayoría de los ejemplos de este documento se usa `ConvertFrom-Json` toodisplay elementos de documento de respuesta de Hola Hola [configuración de actualización Ambari](#example-update-ambari-configuration) en el ejemplo se utiliza jq.</span><span class="sxs-lookup"><span data-stu-id="44327-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="44327-152">Jq se utiliza en este ejemplo tooconstruct una nueva plantilla de documento de respuesta JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="44327-153">Para obtener una referencia completa de hello API de REST, consulte [V1 de referencia de API de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="44327-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="44327-154">Ejemplo: Obtener Hola FQDN de nodos de clúster</span><span class="sxs-lookup"><span data-stu-id="44327-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="44327-155">Cuando se trabaja con HDInsight, necesita el nombre de dominio completo de Hola de tooknow (FQDN) de un nodo de clúster.</span><span class="sxs-lookup"><span data-stu-id="44327-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="44327-156">Puede recuperar con facilidad hello FQDN para saludo diversos nodos de clúster de hello mediante hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="44327-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="44327-157">**Todos los nodos**</span><span class="sxs-lookup"><span data-stu-id="44327-157">**All nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* <span data-ttu-id="44327-158">**Nodos principales**</span><span class="sxs-lookup"><span data-stu-id="44327-158">**Head nodes**</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="44327-159">**Nodos de trabajo**</span><span class="sxs-lookup"><span data-stu-id="44327-159">**Worker nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* <span data-ttu-id="44327-160">**Nodos de Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="44327-160">**Zookeeper nodes**</span></span>

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="44327-161">Ejemplo: Obtener la dirección IP interna de Hola de nodos de clúster</span><span class="sxs-lookup"><span data-stu-id="44327-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44327-162">direcciones IP de Hello devueltas en los ejemplos de hello en esta sección están no directamente accesible over Hola internet.</span><span class="sxs-lookup"><span data-stu-id="44327-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="44327-163">Solo están accesibles desde la red Virtual de Azure que contiene el clúster de HDInsight de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="44327-164">Para obtener más información sobre el uso de HDInsight y de las redes virtuales, vea [Extensión de las funcionalidades de HDInsight con una red virtual de Azure personalizada](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="44327-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="44327-165">dirección IP de toofind hello, debe conocer el nombre de dominio completo interno de hello (FQDN) del programa Hola a los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="44327-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="44327-166">Una vez que tenga Hola FQDN, a continuación, puede obtener dirección IP de Hola de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="44327-167">Hello en los ejemplos siguientes primero consultan Ambari Hola FQDN de todos los nodos de host de Hola y consultan Ambari para la dirección IP de Hola de cada host.</span><span class="sxs-lookup"><span data-stu-id="44327-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="44327-168">Ejemplo: Obtener almacenamiento predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="44327-168">Example: Get hello default storage</span></span>

<span data-ttu-id="44327-169">Cuando se crea un clúster de HDInsight, debe usar una cuenta de almacenamiento de Azure o un almacén de Data Lake como almacenamiento predeterminado de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="44327-170">Puede usar Ambari tooretrieve esta información una vez creado el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="44327-171">Por ejemplo, si desea que el contenedor de toohello tooread/escritura datos fuera de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44327-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="44327-172">Hello en los ejemplos siguientes recuperan configuración de almacenamiento predeterminada de Hola Hola clúster de:</span><span class="sxs-lookup"><span data-stu-id="44327-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> <span data-ttu-id="44327-173">Estos ejemplos devuelven Hola primer servidor de toohello de configuración que se aplica (`service_config_version=1`) que contiene esta información.</span><span class="sxs-lookup"><span data-stu-id="44327-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="44327-174">Si recupera un valor que se ha modificado después de la creación del clúster, puede necesita toolist Hola configuración versiones y recuperar hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="44327-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="44327-175">valor devuelto de Hello es tooone similar de hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="44327-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="44327-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Este valor indica que ese clúster Hola está usando una cuenta de almacenamiento de Azure para el almacenamiento de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="44327-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="44327-177">Hola `ACCOUNTNAME` valor es Hola nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="44327-178">Hola `CONTAINER` parte es el nombre de Hola Hola del contenedor de blobs en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="44327-179">contenedor de Hello es la raíz de Hola de almacenamiento compatible HDFS del clúster Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="44327-180">`adl://home`-Este valor indica que ese clúster Hola está usando un almacén de Data Lake de Azure para el almacenamiento de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="44327-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="44327-181">nombre de cuenta de almacén de Data Lake de toofind hello, Hola de uso en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="44327-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    <span data-ttu-id="44327-182">Hello valor devuelto es similar demasiado`ACCOUNTNAME.azuredatalakestore.net`, donde `ACCOUNTNAME` es Hola nombre de cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="44327-183">directorio de hello toofind dentro de almacén de Data Lake que contiene almacenamiento Hola Hola del clúster, Hola de uso en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="44327-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    <span data-ttu-id="44327-184">Hello valor devuelto es similar demasiado`/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="44327-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="44327-185">Este valor es una ruta de acceso dentro de la cuenta de almacén de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="44327-186">Esta ruta de acceso es la raíz de Hola de hello HDFS compatible filesystem para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="44327-187">Hola `Get-AzureRmHDInsightCluster` cmdlet proporcionado por [Azure PowerShell](/powershell/azure/overview) también devuelve Hola información de almacenamiento de clúster en Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="44327-188">Ejemplo: Obtener configuración</span><span class="sxs-lookup"><span data-stu-id="44327-188">Example: Get configuration</span></span>

1. <span data-ttu-id="44327-189">Obtener las configuraciones de Hola que están disponibles para el clúster.</span><span class="sxs-lookup"><span data-stu-id="44327-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="44327-190">Este ejemplo devuelve un documento JSON que contiene la configuración actual de hello (identificada por hello *etiqueta* valor) para los componentes de hello instalados en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="44327-191">Hello ejemplo siguiente es un extracto de datos de hello devueltos desde un tipo de clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="44327-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. <span data-ttu-id="44327-192">Obtiene la configuración de hello para el componente de Hola que le interesa.</span><span class="sxs-lookup"><span data-stu-id="44327-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="44327-193">Hola siguiente ejemplo, reemplace `INITIAL` con el valor de etiqueta de hello procedente de la solicitud anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="44327-194">Este ejemplo devuelve un documento JSON que contiene la configuración actual de Hola Hola `core-site` componente.</span><span class="sxs-lookup"><span data-stu-id="44327-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="44327-195">Ejemplo: Actualizar la configuración</span><span class="sxs-lookup"><span data-stu-id="44327-195">Example: Update configuration</span></span>

1. <span data-ttu-id="44327-196">Obtener la configuración actual de hello, que Ambari se almacena como Hola "configuración deseada":</span><span class="sxs-lookup"><span data-stu-id="44327-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="44327-197">Este ejemplo devuelve un documento JSON que contiene la configuración actual de hello (identificada por hello *etiqueta* valor) para los componentes de hello instalados en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="44327-198">Hello ejemplo siguiente es un extracto de datos de hello devueltos desde un tipo de clúster de Spark.</span><span class="sxs-lookup"><span data-stu-id="44327-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    <span data-ttu-id="44327-199">En esta lista, necesita toocopy Hola nombre del componente de hello (por ejemplo, **spark\_thrift\_sparkconf** hello y **etiqueta** valor.</span><span class="sxs-lookup"><span data-stu-id="44327-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="44327-200">Recuperar configuración hello para el componente de Hola y etiqueta mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="44327-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > <span data-ttu-id="44327-201">Reemplace **sparkconf de thrift de spark** y **inicial** en el componente de Hola y etiquetas que desee que la configuración de hello tooretrieve para.</span><span class="sxs-lookup"><span data-stu-id="44327-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="44327-202">Jq son los datos de hello tooturn usado recuperados desde HDInsight en una nueva plantilla de configuración.</span><span class="sxs-lookup"><span data-stu-id="44327-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="44327-203">En concreto, estos ejemplos realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="44327-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="44327-204">Crea un valor único que contiene la cadena de Hola "versión" y la fecha de hello, que se almacena en `newtag`.</span><span class="sxs-lookup"><span data-stu-id="44327-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="44327-205">Crea un documento de raíz para la nueva configuración deseada de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="44327-206">Obtiene Hola contenido de hello `.items[]` de matriz y lo agrega a hello **desired_config** elemento.</span><span class="sxs-lookup"><span data-stu-id="44327-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="44327-207">Hola eliminaciones `href`, `version`, y `Config` elementos, como estos elementos no están necesario toosubmit una nueva configuración.</span><span class="sxs-lookup"><span data-stu-id="44327-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="44327-208">Agrega un nuevo elemento `tag` con un valor de `version#################`.</span><span class="sxs-lookup"><span data-stu-id="44327-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="44327-209">parte numérica de Hola se basa en hello fecha actual.</span><span class="sxs-lookup"><span data-stu-id="44327-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="44327-210">Cada configuración debe tener una etiqueta única.</span><span class="sxs-lookup"><span data-stu-id="44327-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="44327-211">Por último, se guardan los datos de hello toohello `newconfig.json` documento.</span><span class="sxs-lookup"><span data-stu-id="44327-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="44327-212">estructura del documento Hola debe aparecer similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44327-212">hello document structure should appear similar toohello following example:</span></span>
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. <span data-ttu-id="44327-213">Abra hello `newconfig.json` documento y agregar o modificar valores de hello `properties` objeto.</span><span class="sxs-lookup"><span data-stu-id="44327-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="44327-214">ejemplo siguiente se cambia Hola Hola valo `"spark.yarn.am.memory"` de `"1g"` demasiado`"3g"`.</span><span class="sxs-lookup"><span data-stu-id="44327-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="44327-215">También agrega `"spark.kryoserializer.buffer.max"` con un valor de `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="44327-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="44327-216">Guardar archivo hello cuando haya terminado de realizar modificaciones.</span><span class="sxs-lookup"><span data-stu-id="44327-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="44327-217">Usar hello después comandos toosubmit Hola actualizar configuración tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="44327-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    <span data-ttu-id="44327-218">Estos comandos enviar contenido Hola de hello **newconfig.json** archivo toohello clúster Hola configuración deseado de nuevo.</span><span class="sxs-lookup"><span data-stu-id="44327-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="44327-219">solicitud de Hello devuelve un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="44327-219">hello request returns a JSON document.</span></span> <span data-ttu-id="44327-220">Hola **versionTag** elemento en este documento debe coincidir con la versión de Hola envía y Hola **configuraciones** objeto contiene los cambios de configuración de hello solicitado.</span><span class="sxs-lookup"><span data-stu-id="44327-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="44327-221">Ejemplo: Reiniciar un componente de servicio</span><span class="sxs-lookup"><span data-stu-id="44327-221">Example: Restart a service component</span></span>

<span data-ttu-id="44327-222">En este momento, si mira en la interfaz de usuario de web de Ambari hello, Hola servicio de Spark indica que requiere toobe reiniciarse para que apliquen la nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="44327-223">Usar hello después pasos toorestart Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="44327-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="44327-224">Usar hello después tooenable de modo de mantenimiento para el servicio de Spark hello:</span><span class="sxs-lookup"><span data-stu-id="44327-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    <span data-ttu-id="44327-225">Estos comandos de envío de un servidor de toohello de documento JSON que activa el modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="44327-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="44327-226">Puede comprobar que servicio Hola ahora está en modo de mantenimiento usando Hola después de solicitud:</span><span class="sxs-lookup"><span data-stu-id="44327-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    <span data-ttu-id="44327-227">Hello valor devuelto es `ON`.</span><span class="sxs-lookup"><span data-stu-id="44327-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="44327-228">A continuación, usar hello después tooturn desactivar servicio hello:</span><span class="sxs-lookup"><span data-stu-id="44327-228">Next, use hello following tooturn off hello service:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    <span data-ttu-id="44327-229">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="44327-229">hello response is similar toohello following example:</span></span>
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > <span data-ttu-id="44327-230">Hola `href` valor devuelto por este identificador URI está usando la dirección IP interna de Hola Hola del nodo de clúster.</span><span class="sxs-lookup"><span data-stu-id="44327-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="44327-231">toouse desde el clúster fuera de hello, reemplazar parte de hello '10.0.0.18:8080' con el FQDN del clúster de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="44327-232">Hola, siga los comandos recuperar el estado de Hola de solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="44327-232">hello following commands retrieve hello status of hello request:</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    <span data-ttu-id="44327-233">Una respuesta de `COMPLETED` indica que la solicitud Hola ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="44327-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="44327-234">Cuando se completa la solicitud anterior de hello, utilice Hola después toostart Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="44327-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    <span data-ttu-id="44327-235">servicio de Hello ahora está usando la nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="44327-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="44327-236">Por último, utilice Hola después tooturn desactiva el modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="44327-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a><span data-ttu-id="44327-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44327-237">Next steps</span></span>

<span data-ttu-id="44327-238">Para obtener una referencia completa de hello API de REST, consulte [V1 de referencia de API de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="44327-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

