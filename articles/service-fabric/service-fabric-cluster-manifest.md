---
title: "aaaConfigure el clúster de independiente de Azure Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure su clúster de Service Fabric privado o independiente."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="01a9d-103">Opciones de configuración de clústeres de Windows independientes</span><span class="sxs-lookup"><span data-stu-id="01a9d-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="01a9d-104">Este artículo describe cómo tooconfigure un clúster de Service Fabric independientes con Hola ***ClusterConfig.JSON*** archivo.</span><span class="sxs-lookup"><span data-stu-id="01a9d-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="01a9d-105">Puede utilizar esta información de toospecify de archivo como nodos de Service Fabric hello y sus direcciones IP, los distintos tipos de nodos en clúster hello, las configuraciones de seguridad de hello, así como la topología de red de hello en cuanto a dominios de error o una actualización, para su independiente clúster.</span><span class="sxs-lookup"><span data-stu-id="01a9d-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="01a9d-106">Cuando se [Descargar paquete de Service Fabric independiente de hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), algunos ejemplos de archivo de hello ClusterConfig.JSON son tooyour descargado trabajo máquina.</span><span class="sxs-lookup"><span data-stu-id="01a9d-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="01a9d-107">ejemplos de Hello tener *DevCluster* en sus nombres le ayudará a crear un clúster con todos los tres nodos en hello mismo equipo, como nodos lógicos.</span><span class="sxs-lookup"><span data-stu-id="01a9d-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="01a9d-108">Fuera de estos casos, al menos un nodo debe marcarse como un nodo principal.</span><span class="sxs-lookup"><span data-stu-id="01a9d-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="01a9d-109">Este clúster es útil para un entorno de desarrollo o pruebas y no se admite como clúster de producción.</span><span class="sxs-lookup"><span data-stu-id="01a9d-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="01a9d-110">ejemplos de Hello tener *MultiMachine* en sus nombres, le ayudará a crear un clúster de calidad de producción, donde cada nodo en un equipo independiente.</span><span class="sxs-lookup"><span data-stu-id="01a9d-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="01a9d-111">*ClusterConfig.Unsecure.DevCluster.JSON* y *ClusterConfig.Unsecure.MultiMachine.JSON* mostrar cómo toocreate una prueba no segura o producción de clúster respectivamente.</span><span class="sxs-lookup"><span data-stu-id="01a9d-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="01a9d-112">*ClusterConfig.Windows.DevCluster.JSON* y *ClusterConfig.Windows.MultiMachine.JSON* mostrar cómo toocreate clúster de prueba o de producción, proteger mediante [la seguridad de Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="01a9d-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="01a9d-113">*ClusterConfig.X509.DevCluster.JSON* y *ClusterConfig.X509.MultiMachine.JSON* mostrar cómo toocreate clúster de prueba o de producción, proteger mediante [X509 seguridad basada en certificados](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="01a9d-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="01a9d-114">Ahora examinaremos Hola distintas secciones de un ***ClusterConfig.JSON*** de archivos como sigue.</span><span class="sxs-lookup"><span data-stu-id="01a9d-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="01a9d-115">Opciones generales de configuración de clústeres</span><span class="sxs-lookup"><span data-stu-id="01a9d-115">General cluster configurations</span></span>
<span data-ttu-id="01a9d-116">Esto cubre Hola clúster amplia configuraciones específicas de tal como se muestra en el siguiente fragmento de JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="01a9d-117">Puede proporcionar cualquier clúster de Service Fabric Nombre_descriptivo tooyour asignando toohello **nombre** variable.</span><span class="sxs-lookup"><span data-stu-id="01a9d-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="01a9d-118">Hola **clusterConfigurationVersion** es el número de versión de Hola del clúster; debe aumentar cada vez que actualice el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="01a9d-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="01a9d-119">Sin embargo, que debe conservarse hello **el elemento apiVersion** toohello por defecto.</span><span class="sxs-lookup"><span data-stu-id="01a9d-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="01a9d-120">Nodos de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="01a9d-120">Nodes on hello cluster</span></span>
<span data-ttu-id="01a9d-121">Puede configurar los nodos de hello en el clúster de Service Fabric mediante hello **nodos** sección, como el fragmento siguiente muestra de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="01a9d-122">Un clúster de Service Fabric debe contener al menos 3 nodos.</span><span class="sxs-lookup"><span data-stu-id="01a9d-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="01a9d-123">Puede agregar más sección toothis de nodos según el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="01a9d-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="01a9d-124">Hello en la tabla siguiente explica los valores de configuración de Hola para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="01a9d-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="01a9d-125">**Opción de configuración del nodo**</span><span class="sxs-lookup"><span data-stu-id="01a9d-125">**Node configuration**</span></span> | <span data-ttu-id="01a9d-126">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="01a9d-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="01a9d-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="01a9d-127">nodeName</span></span> |<span data-ttu-id="01a9d-128">Puede permitir que cualquier nodo de toohello nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="01a9d-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="01a9d-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="01a9d-129">iPAddress</span></span> |<span data-ttu-id="01a9d-130">Obtener dirección IP de hello del nodo, abra una ventana de comandos y escriba `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="01a9d-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="01a9d-131">Tenga en cuenta dirección IPV4 de Hola y asignar toohello **iPAddress** variable.</span><span class="sxs-lookup"><span data-stu-id="01a9d-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="01a9d-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="01a9d-132">nodeTypeRef</span></span> |<span data-ttu-id="01a9d-133">Cada nodo se puede asignar a un tipo de nodo diferente.</span><span class="sxs-lookup"><span data-stu-id="01a9d-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="01a9d-134">Hola [tipos de nodos](#nodetypes) se definen en la siguiente sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="01a9d-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="01a9d-135">faultDomain</span></span> |<span data-ttu-id="01a9d-136">Error dominios habilitar administradores toodefine Hola físicos nodos de clúster que podrían producir un error en hello mismo tiempo debido a dependencias físico tooshared.</span><span class="sxs-lookup"><span data-stu-id="01a9d-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="01a9d-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="01a9d-137">upgradeDomain</span></span> |<span data-ttu-id="01a9d-138">Dominios de actualización describen los conjuntos de nodos que se cierran de Service Fabric actualiza a sobre Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="01a9d-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="01a9d-139">Puede elegir qué toowhich tooassign de nodos de dominios de actualización, como que no están limitados por los requisitos físicos.</span><span class="sxs-lookup"><span data-stu-id="01a9d-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="01a9d-140">Propiedades de clúster</span><span class="sxs-lookup"><span data-stu-id="01a9d-140">Cluster properties</span></span>
<span data-ttu-id="01a9d-141">Hola **propiedades** sección en hello ClusterConfig.JSON está en clúster de hello tooconfigure usado como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="01a9d-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="01a9d-142">Confiabilidad</span><span class="sxs-lookup"><span data-stu-id="01a9d-142">Reliability</span></span>
<span data-ttu-id="01a9d-143">concepto de Hola de **reliabilityLevel** define número Hola de réplicas o instancias de servicios del sistema de Service Fabric Hola que se pueden ejecutar en nodos principales de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="01a9d-144">Determina la confiabilidad de Hola de estos servicios y, por tanto, Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="01a9d-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="01a9d-145">valor de Hello es calculada por el sistema de hello en tiempo de creación y actualización de clúster.</span><span class="sxs-lookup"><span data-stu-id="01a9d-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="01a9d-146">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="01a9d-146">Diagnostics</span></span>
<span data-ttu-id="01a9d-147">Hola **diagnosticsStore** sección permite diagnósticos de tooconfigure parámetros tooenable y nodo de solución de problemas o errores de clúster, tal y como se muestra en el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="01a9d-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="01a9d-148">Hola **metadatos** es una descripción de los diagnósticos de clúster y se puede establecer según la configuración.</span><span class="sxs-lookup"><span data-stu-id="01a9d-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="01a9d-149">Estas variables permiten recopilar registros de seguimiento ETW, volcados de memoria y contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="01a9d-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="01a9d-150">Lea [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) y [Seguimiento ETW](https://msdn.microsoft.com/library/ms751538.aspx) para más información sobre los registros de seguimiento ETW.</span><span class="sxs-lookup"><span data-stu-id="01a9d-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="01a9d-151">Todos los registros incluidos [volcados de memoria](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) y [contadores de rendimiento](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) puede ser dirigido toohello **connectionString** carpeta en su equipo.</span><span class="sxs-lookup"><span data-stu-id="01a9d-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="01a9d-152">También puede usar *AzureStorage* para almacenar diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="01a9d-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="01a9d-153">Vea a continuación un ejemplo de fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="01a9d-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="01a9d-154">Seguridad</span><span class="sxs-lookup"><span data-stu-id="01a9d-154">Security</span></span>
<span data-ttu-id="01a9d-155">Hola **seguridad** sección es necesario para un clúster de Service Fabric segura independiente.</span><span class="sxs-lookup"><span data-stu-id="01a9d-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="01a9d-156">Hola siguiente fragmento de código muestra una parte de esta sección.</span><span class="sxs-lookup"><span data-stu-id="01a9d-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="01a9d-157">Hola **metadatos** es una descripción de su clúster segura y se pueden establecer según la configuración.</span><span class="sxs-lookup"><span data-stu-id="01a9d-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="01a9d-158">Hola **ClusterCredentialType** y **ServerCredentialType** determinar el tipo de saludo de seguridad que va a implementar clústeres de Hola y nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="01a9d-159">Se pueden establecer tooeither *X509* para una seguridad basada en certificados, o *Windows* una seguridad basada en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01a9d-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="01a9d-160">Hola rest de hello **seguridad** sección se basará en el tipo de saludo de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="01a9d-161">Lectura [seguridad basada en certificados en un clúster independiente](service-fabric-windows-cluster-x509-security.md) o [la seguridad de Windows en un clúster independiente](service-fabric-windows-cluster-windows-security.md) para obtener información sobre cómo se rest toofill out Hola de hello **seguridad**sección.</span><span class="sxs-lookup"><span data-stu-id="01a9d-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="01a9d-162">Tipos de nodo</span><span class="sxs-lookup"><span data-stu-id="01a9d-162">Node Types</span></span>
<span data-ttu-id="01a9d-163">Hola **nodeTypes** sección describe el tipo de Hola de nodos de Hola que tiene el clúster.</span><span class="sxs-lookup"><span data-stu-id="01a9d-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="01a9d-164">Debe especificarse al menos un tipo de nodo de un clúster, tal y como se muestra en el siguiente fragmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="01a9d-165">Hola **nombre** es Hola nombre descriptivo para este tipo de nodo concreto.</span><span class="sxs-lookup"><span data-stu-id="01a9d-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="01a9d-166">toocreate un nodo de este tipo de nodo, asignar su nombre descriptivo toohello **elemento nodeTypeRef** variable para ese nodo, como se mencionó [anteriormente](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="01a9d-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="01a9d-167">Para cada tipo de nodo, definir extremos de la conexión de Hola que va a utilizar.</span><span class="sxs-lookup"><span data-stu-id="01a9d-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="01a9d-168">Puede elegir cualquier número de puerto para estos puntos de conexión, siempre que no entren en conflicto con otros puntos de conexión de este clúster.</span><span class="sxs-lookup"><span data-stu-id="01a9d-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="01a9d-169">En un clúster de varios nodos, habrá uno o más nodos primarios (es decir, **isPrimary** establecido demasiado*true*), en función de hello [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="01a9d-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="01a9d-170">Lectura [consideraciones de planear la capacidad de clúster de Service Fabric](service-fabric-cluster-capacity.md) para obtener información sobre **nodeTypes** y **reliabilityLevel**y tooknow las principales y Hola tipos de nodos no principales.</span><span class="sxs-lookup"><span data-stu-id="01a9d-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="01a9d-171">Los extremos utilizan tipos de nodos de hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="01a9d-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="01a9d-172">*clientConnectionEndpointPort* es el puerto de hello usado Hola cliente tooconnect toohello el clúster, al usar las API de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="01a9d-173">*clusterConnectionEndpointPort* es el puerto de hello en el que los nodos de hello comunican entre sí.</span><span class="sxs-lookup"><span data-stu-id="01a9d-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="01a9d-174">*leaseDriverEndpointPort* es el puerto de hello utilizada por hello clúster concesión controlador toofind out si nodos Hola siguen estando activos.</span><span class="sxs-lookup"><span data-stu-id="01a9d-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="01a9d-175">*serviceConnectionEndpointPort* es el puerto de hello usado por aplicaciones de Hola y servicios implementados en un nodo, toocommunicate con cliente de Service Fabric hello en ese nodo concreto.</span><span class="sxs-lookup"><span data-stu-id="01a9d-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="01a9d-176">*httpGatewayEndpointPort* es el puerto de hello usado Hola Service Fabric Explorer tooconnect toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="01a9d-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="01a9d-177">*ephemeralPorts* invalidar hello [puertos dinámicos utilizados Hola OS](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="01a9d-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="01a9d-178">Service Fabric utilizará una parte de ellos como puertos de la aplicación y Hola restantes estarán disponibles para hello SO.</span><span class="sxs-lookup"><span data-stu-id="01a9d-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="01a9d-179">También asignará este intervalo toohello existente intervalo presente en Hola de sistema operativo, por lo que para todos los propósitos, se pueden usar intervalos de hello en archivos JSON de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="01a9d-180">Debe asegurarse de que diferencia Hola entre puertos Hola y de inicio de hello es al menos de 255 toomake.</span><span class="sxs-lookup"><span data-stu-id="01a9d-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="01a9d-181">Puede encontrarse con conflictos si esta diferencia es demasiado baja, ya que este intervalo se comparte con el sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="01a9d-182">Ver el intervalo de puertos dinámicos de hello configurado ejecutando `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="01a9d-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="01a9d-183">*applicationPorts* son puertos Hola que se usará en las aplicaciones de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="01a9d-184">intervalo de puertos de aplicación Hola debe ser el requisito de punto de conexión de hello toocover lo suficientemente grande como de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="01a9d-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="01a9d-185">Este intervalo debe ser exclusivo del intervalo de puertos dinámicos de hello en la máquina de hello, es decir, hello *ephemeralPorts* intervalo como se establece en la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="01a9d-186">Service Fabric utilizará estos siempre que los nuevos puertos son necesarios, así como tener cuidado de abrir firewall de Hola para estos puertos.</span><span class="sxs-lookup"><span data-stu-id="01a9d-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="01a9d-187">*reverseProxyEndpointPort* es un punto de conexión de proxy inverso opcional.</span><span class="sxs-lookup"><span data-stu-id="01a9d-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="01a9d-188">Consulte [Proxy inverso de Service Fabric](service-fabric-reverseproxy.md) para más detalles.</span><span class="sxs-lookup"><span data-stu-id="01a9d-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="01a9d-189">Configuración del registro</span><span class="sxs-lookup"><span data-stu-id="01a9d-189">Log Settings</span></span>
<span data-ttu-id="01a9d-190">Hola **fabricSettings** sección permite tooset Hola raíz directorios de datos de Service Fabric hello y registros.</span><span class="sxs-lookup"><span data-stu-id="01a9d-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="01a9d-191">Puede personalizar estos solo durante la creación de clústeres inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="01a9d-192">Vea el siguiente fragmento de código de ejemplo de esta sección.</span><span class="sxs-lookup"><span data-stu-id="01a9d-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="01a9d-193">Se recomienda usar una unidad no son de SO como hello FabricDataRoot y FabricLogRoot, ya que proporciona más confiabilidad frente a bloqueos de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="01a9d-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="01a9d-194">Tenga en cuenta que si personaliza sólo la raíz de datos hello, a continuación, raíz de registro de hello se colocará un nivel por debajo de la raíz de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a9d-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="01a9d-195">Configuración del servicio de confianza con estado</span><span class="sxs-lookup"><span data-stu-id="01a9d-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="01a9d-196">Hola **KtlLogger** sección permite tooset Hola configuración global de servicios de confianza.</span><span class="sxs-lookup"><span data-stu-id="01a9d-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="01a9d-197">Para obtener más información sobre estas opciones, lea [Configurar Reliable Services con estado](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="01a9d-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="01a9d-198">ejemplo de Hola siguiente muestra cómo toochange Hola Hola compartido registro de transacciones obtiene crea tooback las recopilaciones confiables para los servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="01a9d-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="01a9d-199">Características complementarias</span><span class="sxs-lookup"><span data-stu-id="01a9d-199">Add-on features</span></span>
<span data-ttu-id="01a9d-200">tooconfigure características del complemento, debe ser el elemento apiVersion de hello configurado como ' 04-2017' o superior y addonFeatures necesita toobe configurado:</span><span class="sxs-lookup"><span data-stu-id="01a9d-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="01a9d-201">Compatibilidad con los contenedores</span><span class="sxs-lookup"><span data-stu-id="01a9d-201">Container support</span></span>
<span data-ttu-id="01a9d-202">tooenable compatibilidad con un contenedor para el contenedor de windows server y el contenedor de hyper-v para clústeres independientes, característica que hello 'DnsService' debe toobe habilitado.</span><span class="sxs-lookup"><span data-stu-id="01a9d-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="01a9d-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01a9d-203">Next steps</span></span>
<span data-ttu-id="01a9d-204">Una vez que tenga un archivo ClusterConfig.JSON completo configurado según la configuración de clúster independiente, puede implementar su clúster mediante el siguiente artículo de hello [crear un clúster de Service Fabric independientes](service-fabric-cluster-creation-for-windows-server.md) y, a continuación, continuar demasiado[visualizar el clúster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="01a9d-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

