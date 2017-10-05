---
title: "Extensión de HDInsight con Virtual Network - Azure | Microsoft Docs"
description: Aprenda a usar la Red virtual de Azure para conectar HDInsight con otros recursos en la nube o recursos en su centro de datos.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="779ab-103">Extender Azure HDInsight mediante una instancia de Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="779ab-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="779ab-104">Obtenga información sobre cómo usar HDInsight con una instancia de [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="779ab-105">El uso de una instancia de Azure Virtual Network permite los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="779ab-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="779ab-106">Conectarse a HDInsight directamente desde una red local.</span><span class="sxs-lookup"><span data-stu-id="779ab-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="779ab-107">Conectar HDInsight a almacenes de datos en una instancia de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="779ab-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="779ab-108">Obtener acceso directo a los servicios de Hadoop que no están disponibles públicamente en Internet.</span><span class="sxs-lookup"><span data-stu-id="779ab-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="779ab-109">Por ejemplo, las API de Kafka o la API de Java de HBase.</span><span class="sxs-lookup"><span data-stu-id="779ab-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="779ab-110">La información de este documento requiere conocimientos sobre las redes TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="779ab-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="779ab-111">Si no está familiarizado con las redes TCP/IP, debe asociarse con alguien que lo esté antes de realizar modificaciones a las redes de producción.</span><span class="sxs-lookup"><span data-stu-id="779ab-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="779ab-112">Planificación</span><span class="sxs-lookup"><span data-stu-id="779ab-112">Planning</span></span>

<span data-ttu-id="779ab-113">Debe responder a las preguntas siguientes cuando planee instalar HDInsight en una red virtual:</span><span class="sxs-lookup"><span data-stu-id="779ab-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="779ab-114">¿Necesita instalar HDInsight en una red virtual existente?</span><span class="sxs-lookup"><span data-stu-id="779ab-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="779ab-115">¿O bien está creando una red nueva?</span><span class="sxs-lookup"><span data-stu-id="779ab-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="779ab-116">Si está usando una red virtual existente, puede que tenga que modificar la configuración de red antes de poder instalar HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="779ab-117">Para más información, vea la sección [Agregar HDInsight a una red virtual existente](#existingvnet).</span><span class="sxs-lookup"><span data-stu-id="779ab-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="779ab-118">¿Quiere conectar la red virtual que contiene HDInsight a otra red virtual o a la red local?</span><span class="sxs-lookup"><span data-stu-id="779ab-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="779ab-119">Para trabajar fácilmente con recursos entre redes, puede que tenga que crear un DNS personalizado y configurar el reenvío de DNS.</span><span class="sxs-lookup"><span data-stu-id="779ab-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="779ab-120">Para más información, vea la sección [Conexión de varias redes](#multinet).</span><span class="sxs-lookup"><span data-stu-id="779ab-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="779ab-121">¿Quiere restringir o redirigir el tráfico de entrada o salida a HDInsight?</span><span class="sxs-lookup"><span data-stu-id="779ab-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="779ab-122">HDInsight debe tener comunicación sin restricciones con direcciones IP específicas en el centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="779ab-123">También hay varios puertos que deben permitirse a través de los firewalls para la comunicación del cliente.</span><span class="sxs-lookup"><span data-stu-id="779ab-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="779ab-124">Para más información, vea la sección [Control del tráfico de red](#networktraffic).</span><span class="sxs-lookup"><span data-stu-id="779ab-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="779ab-125"><a id="existingvnet"></a>Agregar HDInsight una red virtual existente</span><span class="sxs-lookup"><span data-stu-id="779ab-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="779ab-126">Use los pasos de esta sección para saber cómo agregar un nuevo HDInsight a una instancia de Azure Virtual Network existente.</span><span class="sxs-lookup"><span data-stu-id="779ab-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="779ab-127">No se puede agregar un clúster de HDInsight existente a una red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="779ab-128">¿Está usando un modelo de implementación clásico o de Resource Manager para la red virtual?</span><span class="sxs-lookup"><span data-stu-id="779ab-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="779ab-129">HDInsight 3.4 y versiones posteriores requieren una red virtual de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="779ab-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="779ab-130">Las versiones anteriores de HDInsight requieren una red virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="779ab-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="779ab-131">Si la red existente es una red virtual clásica, debe crear una red virtual de Resource Manager y después conectar las dos.</span><span class="sxs-lookup"><span data-stu-id="779ab-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="779ab-132">[Conexión de redes virtuales clásicas a redes virtuales nuevas](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="779ab-133">Una vez combinadas, HDInsight instalado en la red de Resource Manager puede interactuar con los recursos de la red clásica.</span><span class="sxs-lookup"><span data-stu-id="779ab-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="779ab-134">¿Usa tunelización forzada?</span><span class="sxs-lookup"><span data-stu-id="779ab-134">Do you use forced tunneling?</span></span> <span data-ttu-id="779ab-135">La tunelización forzada es una configuración de subred que fuerza el tráfico de salida de Internet a un dispositivo para la inspección y el registro.</span><span class="sxs-lookup"><span data-stu-id="779ab-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="779ab-136">HDInsight no es compatible con la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="779ab-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="779ab-137">Quite la tunelización forzada antes de instalar HDInsight en una subred, o bien cree una nueva subred para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="779ab-138">¿Usa grupos de seguridad de red, rutas definidas por el usuario o dispositivos de red virtual para restringir el tráfico de entrada y salida de la red virtual?</span><span class="sxs-lookup"><span data-stu-id="779ab-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="779ab-139">Como servicio administrado, HDInsight requiere acceso sin restricciones a varias direcciones IP en el centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="779ab-140">Para permitir la comunicación con estas direcciones IP, actualice las rutas definidas por el usuario o los grupos de seguridad de red existentes.</span><span class="sxs-lookup"><span data-stu-id="779ab-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="779ab-141">HDInsight hospeda varios servicios, que usan varios puertos.</span><span class="sxs-lookup"><span data-stu-id="779ab-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="779ab-142">No bloquee el tráfico a estos puertos.</span><span class="sxs-lookup"><span data-stu-id="779ab-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="779ab-143">Para obtener una lista de puertos para permitir a través de los firewalls de dispositivo virtual, vea la sección [Seguridad](#security).</span><span class="sxs-lookup"><span data-stu-id="779ab-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="779ab-144">Para buscar la configuración de seguridad existente, use los siguientes comandos de Azure PowerShell o de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="779ab-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="779ab-145">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="779ab-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="779ab-146">Para más información, vea el documento sobre [Solución de problemas de los grupos de seguridad de red](../virtual-network/virtual-network-nsg-troubleshoot-portal.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="779ab-147">Se aplican reglas de grupo de seguridad de red en orden según la prioridad de la regla.</span><span class="sxs-lookup"><span data-stu-id="779ab-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="779ab-148">Se aplica la primera regla que coincide con el patrón de tráfico y no se aplica ninguna otra para el tráfico.</span><span class="sxs-lookup"><span data-stu-id="779ab-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="779ab-149">El orden de las reglas es de más a menos permisiva.</span><span class="sxs-lookup"><span data-stu-id="779ab-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="779ab-150">Para más información, vea el documento [Filtrar el tráfico de red con grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="779ab-151">Rutas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="779ab-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="779ab-152">Para más información, vea el documento sobre [Solución de problemas de rutas](../virtual-network/virtual-network-routes-troubleshoot-portal.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="779ab-153">Cree un clúster de HDInsight y seleccione la instancia de Azure Virtual Network durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="779ab-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="779ab-154">Para entender el proceso de creación de clúster, use los pasos descritos en los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="779ab-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * [<span data-ttu-id="779ab-155">Creación de HDInsight con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="779ab-155">Create HDInsight using the Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="779ab-156">Creación de HDInsight con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="779ab-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="779ab-157">Creación de HDInsight con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="779ab-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="779ab-158">Creación de una instancia de HDInsight mediante el uso de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="779ab-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="779ab-159">Agregar HDInsight a una red virtual es un paso de configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="779ab-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="779ab-160">Asegúrese de seleccionar la red virtual al configurar el clúster.</span><span class="sxs-lookup"><span data-stu-id="779ab-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="779ab-161"><a id="multinet"></a>Conectar varias redes</span><span class="sxs-lookup"><span data-stu-id="779ab-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="779ab-162">El mayor desafío con una configuración de varias redes es la resolución de nombres entre las redes.</span><span class="sxs-lookup"><span data-stu-id="779ab-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="779ab-163">Azure proporciona resolución de nombres para los servicios de Azure instalados en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="779ab-164">Esta resolución de nombres integrada permite conectar HDInsight a los siguientes recursos mediante un nombre de dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="779ab-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="779ab-165">Cualquier recurso que está disponible en Internet.</span><span class="sxs-lookup"><span data-stu-id="779ab-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="779ab-166">Por ejemplo, microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="779ab-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="779ab-167">Cualquier recurso que se encuentre en la misma instancia de Azure Virtual Network, mediante el uso del __nombre DNS interno__ del recurso.</span><span class="sxs-lookup"><span data-stu-id="779ab-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="779ab-168">Por ejemplo, cuando se usa la resolución de nombres predeterminada, los siguientes son nombres DNS internos de ejemplo que se asignan a nodos de trabajo de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="779ab-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="779ab-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="779ab-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="779ab-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="779ab-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="779ab-171">Estos dos nodos pueden comunicarse directamente entre sí y con otros nodos de HDInsight, mediante el uso de nombres DNS internos.</span><span class="sxs-lookup"><span data-stu-id="779ab-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="779ab-172">La resolución de nombres predeterminada __no__ permite que HDInsight resuelva los nombres de recursos en redes que se unen a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="779ab-173">Por ejemplo, es habitual unir la red local a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="779ab-174">Con solo la resolución de nombres predeterminada, HDInsight no puede tener acceso a los recursos de la red local por su nombre.</span><span class="sxs-lookup"><span data-stu-id="779ab-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="779ab-175">Lo contrario también es cierto, los recursos de la red local no pueden tener acceso a recursos de la red virtual por su nombre.</span><span class="sxs-lookup"><span data-stu-id="779ab-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="779ab-176">Debe crear el servidor DNS personalizado y configurar la red virtual para usarla antes de crear el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="779ab-177">Para habilitar la resolución de nombres entre la red virtual y los recursos en redes combinadas, debe realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="779ab-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="779ab-178">Cree un servidor DNS personalizado en la instancia de Azure Virtual Network en la que planea instalar HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="779ab-179">Configure la red virtual para usar el servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="779ab-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="779ab-180">Busque el sufijo DNS que Azure asigna a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="779ab-181">Este valor es similar a `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="779ab-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="779ab-182">Para obtener información sobre cómo buscar el sufijo DNS, vea la sección [Ejemplo: DNS personalizado](#example-dns).</span><span class="sxs-lookup"><span data-stu-id="779ab-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="779ab-183">Configure el reenvío entre los servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="779ab-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="779ab-184">La configuración depende del tipo de red remota.</span><span class="sxs-lookup"><span data-stu-id="779ab-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="779ab-185">Si la red remota es una red local, configure DNS como sigue:</span><span class="sxs-lookup"><span data-stu-id="779ab-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="779ab-186">__DNS personalizado__ (en la red virtual):</span><span class="sxs-lookup"><span data-stu-id="779ab-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="779ab-187">Reenvíe las solicitudes para el sufijo DNS de la red virtual a la resolución recursiva de Azure (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="779ab-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="779ab-188">Azure administra las solicitudes de recursos en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="779ab-189">Reenvíe las demás solicitudes al servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="779ab-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="779ab-190">El servidor DNS local administra todas las solicitudes de resolución de nombres, incluso las de recursos de Internet como Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="779ab-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="779ab-191">__DNS local__: Reenvíe las solicitudes para el sufijo DNS de red virtual al servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="779ab-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="779ab-192">El servidor DNS personalizado reenvía a la resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="779ab-193">Esta configuración dirige las solicitudes de nombres de dominio completos que contienen el sufijo DNS de la red virtual al servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="779ab-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="779ab-194">Todas las demás solicitudes (incluso para las direcciones públicas de Internet) se controlan mediante el servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="779ab-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="779ab-195">Si la red remota es otra instancia de Azure Virtual Network, configure DNS como sigue:</span><span class="sxs-lookup"><span data-stu-id="779ab-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="779ab-196">__DNS personalizado__ (en cada red virtual):</span><span class="sxs-lookup"><span data-stu-id="779ab-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="779ab-197">Las solicitudes para el sufijo DNS de las redes virtuales se reenvían a los servidores DNS personalizados.</span><span class="sxs-lookup"><span data-stu-id="779ab-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="779ab-198">El DNS de cada red virtual es el responsable de resolver los recursos dentro de su red.</span><span class="sxs-lookup"><span data-stu-id="779ab-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="779ab-199">Todas las demás solicitudes se reenvían a la resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="779ab-200">La resolución recursiva es responsable de resolver los recursos locales y de Internet.</span><span class="sxs-lookup"><span data-stu-id="779ab-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="779ab-201">El servidor DNS de cada red reenvía las solicitudes al otro, según el sufijo DNS.</span><span class="sxs-lookup"><span data-stu-id="779ab-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="779ab-202">Las demás solicitudes se resuelven mediante la resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="779ab-203">Para obtener un ejemplo de cada configuración, vea la sección [Ejemplo: DNS personalizado](#example-dns).</span><span class="sxs-lookup"><span data-stu-id="779ab-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="779ab-204">Para más información, vea el documento [Resolución de nombres para máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="779ab-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="779ab-205">Conectar directamente a servicios Hadoop</span><span class="sxs-lookup"><span data-stu-id="779ab-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="779ab-206">En la mayor parte de la documentación sobre HDInsight se supone que tiene acceso al clúster a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="779ab-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="779ab-207">Por ejemplo, que se puede conectar al clúster en https://NOMBREDECLÚSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="779ab-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="779ab-208">Esta dirección usa la puerta de enlace pública, que no está disponible si ha usado NSG o UDR para restringir el acceso desde Internet.</span><span class="sxs-lookup"><span data-stu-id="779ab-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="779ab-209">Para conectarse a Ambari y otras páginas web a través de la red virtual, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="779ab-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="779ab-210">Para detectar los nombres de dominio completos (FQDN) internos de los nodos de clúster de HDInsight, use uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="779ab-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="779ab-211">En la lista de nodos que se devuelve, busque el FQDN de los nodos principales y use los FQDN para conectarse a Ambari y otros servicios web.</span><span class="sxs-lookup"><span data-stu-id="779ab-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="779ab-212">Por ejemplo, use `http://<headnode-fqdn>:8080` para tener acceso a Ambari.</span><span class="sxs-lookup"><span data-stu-id="779ab-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="779ab-213">Algunos servicios hospedados en los nodos principales solo están activos en un nodo a la vez.</span><span class="sxs-lookup"><span data-stu-id="779ab-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="779ab-214">Si intenta obtener acceso a un servicio en un nodo principal y se devuelve un error 404, cambie al otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="779ab-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="779ab-215">Para determinar el nodo y el puerto en que está disponible un servicio, vea el documento [Puertos utilizados por los servicios Hadoop en HDInsight](./hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="779ab-216"><a id="networktraffic"></a> Control del tráfico de red</span><span class="sxs-lookup"><span data-stu-id="779ab-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="779ab-217">El tráfico de red en instancias de Azure Virtual Network se puede controlar mediante los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="779ab-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="779ab-218">Los **Grupos de seguridad de red** (NSG) permiten filtrar el tráfico de entrada y salida de la red.</span><span class="sxs-lookup"><span data-stu-id="779ab-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="779ab-219">Para más información, vea el documento [Filtrar el tráfico de red con grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="779ab-220">HDInsight no admite la restricción de tráfico saliente.</span><span class="sxs-lookup"><span data-stu-id="779ab-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="779ab-221">Las **Rutas definidas por el usuario** (UDR) definen cómo fluye el tráfico entre los recursos de la red.</span><span class="sxs-lookup"><span data-stu-id="779ab-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="779ab-222">Para más información, vea el documento [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="779ab-223">Los **Dispositivos de red virtual** replican las funciones de dispositivos como enrutadores y firewalls.</span><span class="sxs-lookup"><span data-stu-id="779ab-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="779ab-224">Para más información, vea el documento [Dispositivos de red](https://azure.microsoft.com/solutions/network-appliances).</span><span class="sxs-lookup"><span data-stu-id="779ab-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="779ab-225">Como servicio administrado, HDInsight requiere acceso sin restricciones a los servicios de mantenimiento y administración de Azure en Azure Cloud.</span><span class="sxs-lookup"><span data-stu-id="779ab-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="779ab-226">Al usar NSG y UDR, debe asegurarse de que estos servicios pueden seguir comunicándose con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="779ab-227">HDInsight expone servicios en varios puertos.</span><span class="sxs-lookup"><span data-stu-id="779ab-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="779ab-228">Cuando se usa un firewall de dispositivo virtual, debe permitir el tráfico en los puertos usados para estos servicios.</span><span class="sxs-lookup"><span data-stu-id="779ab-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="779ab-229">Para más información, vea la sección [Puertos obligatorios].</span><span class="sxs-lookup"><span data-stu-id="779ab-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="779ab-230"><a id="hdinsight-ip"></a> HDInsight con grupos de seguridad de red y rutas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="779ab-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="779ab-231">Si planea usar **grupos de seguridad de red** o **rutas definidas por el usuario** para controlar el tráfico de red, realice las siguientes acciones antes de instalar HDInsight:</span><span class="sxs-lookup"><span data-stu-id="779ab-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="779ab-232">Identificar la región de Azure que va a usar para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="779ab-233">Identificar las direcciones IP requeridas para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="779ab-234">Para más información, vea la sección [Direcciones IP requeridas por HDInsight](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="779ab-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="779ab-235">Cree o modifique los grupos de seguridad de red o las rutas definidas por el usuario para la subred en la que tiene previsto instalar HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="779ab-236">__Grupos de seguridad de red__: permita tráfico de __entrada__ en el puerto __443__ desde las direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="779ab-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="779ab-237">__Rutas definidas por el usuario__: cree una ruta a todas las direcciones IP y establezca el __Tipo del próximo salto__ en __Internet__.</span><span class="sxs-lookup"><span data-stu-id="779ab-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="779ab-238">Para más información sobre grupos de seguridad de red o rutas definidas por el usuario, vea la documentación siguiente:</span><span class="sxs-lookup"><span data-stu-id="779ab-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="779ab-239">Grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="779ab-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="779ab-240">Rutas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="779ab-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="779ab-241">Tunelización forzada</span><span class="sxs-lookup"><span data-stu-id="779ab-241">Forced tunneling</span></span>

<span data-ttu-id="779ab-242">La tunelización forzada es una configuración de enrutamiento definida por el usuario en la que todo el tráfico de subred se fuerza a una red o ubicación específica, por ejemplo, la red local.</span><span class="sxs-lookup"><span data-stu-id="779ab-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="779ab-243">HDInsight __no__ es compatible con la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="779ab-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="779ab-244"><a id="hdinsight-ip"></a> Direcciones IP necesarias</span><span class="sxs-lookup"><span data-stu-id="779ab-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="779ab-245">Los servicios de mantenimiento y administración de Azure deben poder comunicarse con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="779ab-246">Si utiliza grupos de seguridad de red o rutas definidas por el usuario, permita el tráfico de las direcciones IP a estos servicios para llegar a HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="779ab-247">Si no usa grupos de seguridad de red ni rutas definidas por el usuario para controlar el tráfico, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="779ab-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="779ab-248">Si usa grupos de seguridad de red o rutas definidas por el usuario, debe permitir que el tráfico de los servicios de mantenimiento y administración de Azure llegue a HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="779ab-249">Siga los pasos siguientes para buscar las direcciones IP que se deben permitir:</span><span class="sxs-lookup"><span data-stu-id="779ab-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="779ab-250">Siempre debe permitir el tráfico de las siguientes direcciones IP:</span><span class="sxs-lookup"><span data-stu-id="779ab-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="779ab-251">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="779ab-251">IP address</span></span> | <span data-ttu-id="779ab-252">Puerto permitido</span><span class="sxs-lookup"><span data-stu-id="779ab-252">Allowed port</span></span> | <span data-ttu-id="779ab-253">Dirección</span><span class="sxs-lookup"><span data-stu-id="779ab-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="779ab-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="779ab-254">168.61.49.99</span></span> | <span data-ttu-id="779ab-255">443</span><span class="sxs-lookup"><span data-stu-id="779ab-255">443</span></span> | <span data-ttu-id="779ab-256">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-256">Inbound</span></span> |
    | <span data-ttu-id="779ab-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="779ab-257">23.99.5.239</span></span> | <span data-ttu-id="779ab-258">443</span><span class="sxs-lookup"><span data-stu-id="779ab-258">443</span></span> | <span data-ttu-id="779ab-259">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-259">Inbound</span></span> |
    | <span data-ttu-id="779ab-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="779ab-260">168.61.48.131</span></span> | <span data-ttu-id="779ab-261">443</span><span class="sxs-lookup"><span data-stu-id="779ab-261">443</span></span> | <span data-ttu-id="779ab-262">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-262">Inbound</span></span> |
    | <span data-ttu-id="779ab-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="779ab-263">138.91.141.162</span></span> | <span data-ttu-id="779ab-264">443</span><span class="sxs-lookup"><span data-stu-id="779ab-264">443</span></span> | <span data-ttu-id="779ab-265">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-265">Inbound</span></span> |

2. <span data-ttu-id="779ab-266">Si el clúster de HDInsight está en una de las siguientes regiones, debe permitir el tráfico de las direcciones IP mostradas para la región:</span><span class="sxs-lookup"><span data-stu-id="779ab-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="779ab-267">Si la región de Azure que está usando no aparece, use únicamente las cuatro direcciones IP del paso 1.</span><span class="sxs-lookup"><span data-stu-id="779ab-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="779ab-268">País</span><span class="sxs-lookup"><span data-stu-id="779ab-268">Country</span></span> | <span data-ttu-id="779ab-269">Region</span><span class="sxs-lookup"><span data-stu-id="779ab-269">Region</span></span> | <span data-ttu-id="779ab-270">Direcciones IP permitidas</span><span class="sxs-lookup"><span data-stu-id="779ab-270">Allowed IP addresses</span></span> | <span data-ttu-id="779ab-271">Puerto permitido</span><span class="sxs-lookup"><span data-stu-id="779ab-271">Allowed port</span></span> | <span data-ttu-id="779ab-272">Dirección</span><span class="sxs-lookup"><span data-stu-id="779ab-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="779ab-273">Asia</span><span class="sxs-lookup"><span data-stu-id="779ab-273">Asia</span></span> | <span data-ttu-id="779ab-274">Asia oriental</span><span class="sxs-lookup"><span data-stu-id="779ab-274">East Asia</span></span> | <span data-ttu-id="779ab-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="779ab-275">23.102.235.122</span></span></br><span data-ttu-id="779ab-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="779ab-276">52.175.38.134</span></span> | <span data-ttu-id="779ab-277">443</span><span class="sxs-lookup"><span data-stu-id="779ab-277">443</span></span> | <span data-ttu-id="779ab-278">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-279">Sudeste asiático</span><span class="sxs-lookup"><span data-stu-id="779ab-279">Southeast Asia</span></span> | <span data-ttu-id="779ab-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="779ab-280">13.76.245.160</span></span></br><span data-ttu-id="779ab-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="779ab-281">13.76.136.249</span></span> | <span data-ttu-id="779ab-282">443</span><span class="sxs-lookup"><span data-stu-id="779ab-282">443</span></span> | <span data-ttu-id="779ab-283">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-283">Inbound</span></span> |
    | <span data-ttu-id="779ab-284">Australia</span><span class="sxs-lookup"><span data-stu-id="779ab-284">Australia</span></span> | <span data-ttu-id="779ab-285">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="779ab-285">Australia East</span></span> | <span data-ttu-id="779ab-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="779ab-286">104.210.84.115</span></span></br><span data-ttu-id="779ab-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="779ab-287">13.75.152.195</span></span> | <span data-ttu-id="779ab-288">443</span><span class="sxs-lookup"><span data-stu-id="779ab-288">443</span></span> | <span data-ttu-id="779ab-289">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-290">Sudeste de Australia</span><span class="sxs-lookup"><span data-stu-id="779ab-290">Australia Southeast</span></span> | <span data-ttu-id="779ab-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="779ab-291">13.77.2.56</span></span></br><span data-ttu-id="779ab-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="779ab-292">13.77.2.94</span></span> | <span data-ttu-id="779ab-293">443</span><span class="sxs-lookup"><span data-stu-id="779ab-293">443</span></span> | <span data-ttu-id="779ab-294">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-294">Inbound</span></span> |
    | <span data-ttu-id="779ab-295">Brasil</span><span class="sxs-lookup"><span data-stu-id="779ab-295">Brazil</span></span> | <span data-ttu-id="779ab-296">Sur de Brasil</span><span class="sxs-lookup"><span data-stu-id="779ab-296">Brazil South</span></span> | <span data-ttu-id="779ab-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="779ab-297">191.235.84.104</span></span></br><span data-ttu-id="779ab-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="779ab-298">191.235.87.113</span></span> | <span data-ttu-id="779ab-299">443</span><span class="sxs-lookup"><span data-stu-id="779ab-299">443</span></span> | <span data-ttu-id="779ab-300">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-300">Inbound</span></span> |
    | <span data-ttu-id="779ab-301">Canadá</span><span class="sxs-lookup"><span data-stu-id="779ab-301">Canada</span></span> | <span data-ttu-id="779ab-302">Este de Canadá</span><span class="sxs-lookup"><span data-stu-id="779ab-302">Canada East</span></span> | <span data-ttu-id="779ab-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="779ab-303">52.229.127.96</span></span></br><span data-ttu-id="779ab-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="779ab-304">52.229.123.172</span></span> | <span data-ttu-id="779ab-305">443</span><span class="sxs-lookup"><span data-stu-id="779ab-305">443</span></span> | <span data-ttu-id="779ab-306">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-307">Centro de Canadá</span><span class="sxs-lookup"><span data-stu-id="779ab-307">Canada Central</span></span> | <span data-ttu-id="779ab-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="779ab-308">52.228.37.66</span></span></br><span data-ttu-id="779ab-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="779ab-309">52.228.45.222</span></span> | <span data-ttu-id="779ab-310">443</span><span class="sxs-lookup"><span data-stu-id="779ab-310">443</span></span> | <span data-ttu-id="779ab-311">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-311">Inbound</span></span> |
    | <span data-ttu-id="779ab-312">China</span><span class="sxs-lookup"><span data-stu-id="779ab-312">China</span></span> | <span data-ttu-id="779ab-313">Norte de China</span><span class="sxs-lookup"><span data-stu-id="779ab-313">China North</span></span> | <span data-ttu-id="779ab-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="779ab-314">42.159.96.170</span></span></br><span data-ttu-id="779ab-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="779ab-315">139.217.2.219</span></span> | <span data-ttu-id="779ab-316">443</span><span class="sxs-lookup"><span data-stu-id="779ab-316">443</span></span> | <span data-ttu-id="779ab-317">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-318">Este de China</span><span class="sxs-lookup"><span data-stu-id="779ab-318">China East</span></span> | <span data-ttu-id="779ab-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="779ab-319">42.159.198.178</span></span></br><span data-ttu-id="779ab-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="779ab-320">42.159.234.157</span></span> | <span data-ttu-id="779ab-321">443</span><span class="sxs-lookup"><span data-stu-id="779ab-321">443</span></span> | <span data-ttu-id="779ab-322">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-322">Inbound</span></span> |
    | <span data-ttu-id="779ab-323">Europa</span><span class="sxs-lookup"><span data-stu-id="779ab-323">Europe</span></span> | <span data-ttu-id="779ab-324">Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="779ab-324">North Europe</span></span> | <span data-ttu-id="779ab-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="779ab-325">52.164.210.96</span></span></br><span data-ttu-id="779ab-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="779ab-326">13.74.153.132</span></span> | <span data-ttu-id="779ab-327">443</span><span class="sxs-lookup"><span data-stu-id="779ab-327">443</span></span> | <span data-ttu-id="779ab-328">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-329">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="779ab-329">West Europe</span></span>| <span data-ttu-id="779ab-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="779ab-330">52.166.243.90</span></span></br><span data-ttu-id="779ab-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="779ab-331">52.174.36.244</span></span> | <span data-ttu-id="779ab-332">443</span><span class="sxs-lookup"><span data-stu-id="779ab-332">443</span></span> | <span data-ttu-id="779ab-333">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-333">Inbound</span></span> |
    | <span data-ttu-id="779ab-334">Alemania</span><span class="sxs-lookup"><span data-stu-id="779ab-334">Germany</span></span> | <span data-ttu-id="779ab-335">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="779ab-335">Germany Central</span></span> | <span data-ttu-id="779ab-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="779ab-336">51.4.146.68</span></span></br><span data-ttu-id="779ab-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="779ab-337">51.4.146.80</span></span> | <span data-ttu-id="779ab-338">443</span><span class="sxs-lookup"><span data-stu-id="779ab-338">443</span></span> | <span data-ttu-id="779ab-339">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-340">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="779ab-340">Germany Northeast</span></span> | <span data-ttu-id="779ab-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="779ab-341">51.5.150.132</span></span></br><span data-ttu-id="779ab-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="779ab-342">51.5.144.101</span></span> | <span data-ttu-id="779ab-343">443</span><span class="sxs-lookup"><span data-stu-id="779ab-343">443</span></span> | <span data-ttu-id="779ab-344">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-344">Inbound</span></span> |
    | <span data-ttu-id="779ab-345">India</span><span class="sxs-lookup"><span data-stu-id="779ab-345">India</span></span> | <span data-ttu-id="779ab-346">India Central</span><span class="sxs-lookup"><span data-stu-id="779ab-346">Central India</span></span> | <span data-ttu-id="779ab-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="779ab-347">52.172.153.209</span></span></br><span data-ttu-id="779ab-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="779ab-348">52.172.152.49</span></span> | <span data-ttu-id="779ab-349">443</span><span class="sxs-lookup"><span data-stu-id="779ab-349">443</span></span> | <span data-ttu-id="779ab-350">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-350">Inbound</span></span> |
    | <span data-ttu-id="779ab-351">Japón</span><span class="sxs-lookup"><span data-stu-id="779ab-351">Japan</span></span> | <span data-ttu-id="779ab-352">Este de Japón</span><span class="sxs-lookup"><span data-stu-id="779ab-352">Japan East</span></span> | <span data-ttu-id="779ab-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="779ab-353">13.78.125.90</span></span></br><span data-ttu-id="779ab-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="779ab-354">13.78.89.60</span></span> | <span data-ttu-id="779ab-355">443</span><span class="sxs-lookup"><span data-stu-id="779ab-355">443</span></span> | <span data-ttu-id="779ab-356">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-357">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="779ab-357">Japan West</span></span> | <span data-ttu-id="779ab-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="779ab-358">40.74.125.69</span></span></br><span data-ttu-id="779ab-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="779ab-359">138.91.29.150</span></span> | <span data-ttu-id="779ab-360">443</span><span class="sxs-lookup"><span data-stu-id="779ab-360">443</span></span> | <span data-ttu-id="779ab-361">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-361">Inbound</span></span> |
    | <span data-ttu-id="779ab-362">Corea</span><span class="sxs-lookup"><span data-stu-id="779ab-362">Korea</span></span> | <span data-ttu-id="779ab-363">Corea Central</span><span class="sxs-lookup"><span data-stu-id="779ab-363">Korea Central</span></span> | <span data-ttu-id="779ab-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="779ab-364">52.231.39.142</span></span></br><span data-ttu-id="779ab-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="779ab-365">52.231.36.209</span></span> | <span data-ttu-id="779ab-366">433</span><span class="sxs-lookup"><span data-stu-id="779ab-366">433</span></span> | <span data-ttu-id="779ab-367">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-368">Corea del Sur</span><span class="sxs-lookup"><span data-stu-id="779ab-368">Korea South</span></span> | <span data-ttu-id="779ab-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="779ab-369">52.231.203.16</span></span></br><span data-ttu-id="779ab-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="779ab-370">52.231.205.214</span></span> | <span data-ttu-id="779ab-371">443</span><span class="sxs-lookup"><span data-stu-id="779ab-371">443</span></span> | <span data-ttu-id="779ab-372">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-372">Inbound</span></span>
    | <span data-ttu-id="779ab-373">Reino Unido</span><span class="sxs-lookup"><span data-stu-id="779ab-373">United Kingdom</span></span> | <span data-ttu-id="779ab-374">Oeste de Reino Unido</span><span class="sxs-lookup"><span data-stu-id="779ab-374">UK West</span></span> | <span data-ttu-id="779ab-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="779ab-375">51.141.13.110</span></span></br><span data-ttu-id="779ab-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="779ab-376">51.141.7.20</span></span> | <span data-ttu-id="779ab-377">443</span><span class="sxs-lookup"><span data-stu-id="779ab-377">443</span></span> | <span data-ttu-id="779ab-378">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-379">Sur del Reino Unido 2</span><span class="sxs-lookup"><span data-stu-id="779ab-379">UK South</span></span> | <span data-ttu-id="779ab-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="779ab-380">51.140.47.39</span></span></br><span data-ttu-id="779ab-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="779ab-381">51.140.52.16</span></span> | <span data-ttu-id="779ab-382">443</span><span class="sxs-lookup"><span data-stu-id="779ab-382">443</span></span> | <span data-ttu-id="779ab-383">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-383">Inbound</span></span> |
    | <span data-ttu-id="779ab-384">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="779ab-384">United States</span></span> | <span data-ttu-id="779ab-385">Central EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="779ab-385">Central US</span></span> | <span data-ttu-id="779ab-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="779ab-386">13.67.223.215</span></span></br><span data-ttu-id="779ab-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="779ab-387">40.86.83.253</span></span> | <span data-ttu-id="779ab-388">443</span><span class="sxs-lookup"><span data-stu-id="779ab-388">443</span></span> | <span data-ttu-id="779ab-389">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-390">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="779ab-390">North Central US</span></span> | <span data-ttu-id="779ab-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="779ab-391">157.56.8.38</span></span></br><span data-ttu-id="779ab-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="779ab-392">157.55.213.99</span></span> | <span data-ttu-id="779ab-393">443</span><span class="sxs-lookup"><span data-stu-id="779ab-393">443</span></span> | <span data-ttu-id="779ab-394">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-395">Centro occidental de EE.UU.</span><span class="sxs-lookup"><span data-stu-id="779ab-395">West Central US</span></span> | <span data-ttu-id="779ab-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="779ab-396">52.161.23.15</span></span></br><span data-ttu-id="779ab-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="779ab-397">52.161.10.167</span></span> | <span data-ttu-id="779ab-398">443</span><span class="sxs-lookup"><span data-stu-id="779ab-398">443</span></span> | <span data-ttu-id="779ab-399">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="779ab-400">Oeste de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="779ab-400">West US 2</span></span> | <span data-ttu-id="779ab-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="779ab-401">52.175.211.210</span></span></br><span data-ttu-id="779ab-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="779ab-402">52.175.222.222</span></span> | <span data-ttu-id="779ab-403">443</span><span class="sxs-lookup"><span data-stu-id="779ab-403">443</span></span> | <span data-ttu-id="779ab-404">Entrada</span><span class="sxs-lookup"><span data-stu-id="779ab-404">Inbound</span></span> |

    <span data-ttu-id="779ab-405">Para más información sobre las direcciones IP que se van a usar para Azure Government, vea el documento [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) (Inteligencia y análisis de Azure Government).</span><span class="sxs-lookup"><span data-stu-id="779ab-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="779ab-406">Si usa un servidor DNS personalizado con la red virtual, también debe permitir el acceso desde __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="779ab-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="779ab-407">Esta es la dirección de la resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="779ab-408">Para más información, vea el documento [Resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="779ab-409">Para más información, vea la sección [Control del tráfico de red](#networktraffic).</span><span class="sxs-lookup"><span data-stu-id="779ab-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="779ab-410"><a id="hdinsight-ports"></a> Puertos necesarios</span><span class="sxs-lookup"><span data-stu-id="779ab-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="779ab-411">Si está planeando usar un **firewall de aplicación virtual** de red para proteger la red virtual, debe permitir el tráfico de salida en los siguientes puertos:</span><span class="sxs-lookup"><span data-stu-id="779ab-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="779ab-412">53</span><span class="sxs-lookup"><span data-stu-id="779ab-412">53</span></span>
* <span data-ttu-id="779ab-413">443</span><span class="sxs-lookup"><span data-stu-id="779ab-413">443</span></span>
* <span data-ttu-id="779ab-414">1433</span><span class="sxs-lookup"><span data-stu-id="779ab-414">1433</span></span>
* <span data-ttu-id="779ab-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="779ab-415">11000-11999</span></span>
* <span data-ttu-id="779ab-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="779ab-416">14000-14999</span></span>

<span data-ttu-id="779ab-417">Para obtener una lista de puertos para servicios específicos, vea el documento [Puertos utilizados por los servicios Hadoop en HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="779ab-418">Para más información sobre las reglas de firewall para aplicaciones virtuales, vea el documento [Escenario de aplicación virtual](../virtual-network/virtual-network-scenario-udr-gw-nva.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="779ab-419"><a id="hdinsight-nsg"></a>Ejemplo: grupos de seguridad de red con HDInsight</span><span class="sxs-lookup"><span data-stu-id="779ab-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="779ab-420">En los ejemplos de esta sección se muestra cómo crear reglas de grupo de seguridad de red que permiten a HDInsight comunicarse con los servicios de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="779ab-421">Antes de usar los ejemplos, ajuste las direcciones IP para que coincidan con las de la región de Azure que esté usando.</span><span class="sxs-lookup"><span data-stu-id="779ab-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="779ab-422">Puede encontrar esta información en la sección [HDInsight con grupos de seguridad de red y rutas definidas por el usuario](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="779ab-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="779ab-423">Plantilla de administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="779ab-423">Azure Resource Management template</span></span>

<span data-ttu-id="779ab-424">La siguiente plantilla de administración de recursos crea una red virtual que restringe el tráfico de entrada pero permite el tráfico desde las direcciones IP requeridas por HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="779ab-425">Esta plantilla crea también un clúster de HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* [<span data-ttu-id="779ab-426">Implementar una instancia segura de Azure Virtual Network y un clúster de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="779ab-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="779ab-427">Cambie las direcciones IP que se usan en este ejemplo para que coincidan con la región de Azure que está usando.</span><span class="sxs-lookup"><span data-stu-id="779ab-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="779ab-428">Puede encontrar esta información en la sección [HDInsight con grupos de seguridad de red y rutas definidas por el usuario](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="779ab-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="779ab-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="779ab-429">Azure PowerShell</span></span>

<span data-ttu-id="779ab-430">Use el siguiente script de PowerShell para crear una red virtual que restringe el tráfico de entrada y permite el tráfico de las direcciones IP para la región de Europa del Norte.</span><span class="sxs-lookup"><span data-stu-id="779ab-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="779ab-431">Cambie las direcciones IP que se usan en este ejemplo para que coincidan con la región de Azure que está usando.</span><span class="sxs-lookup"><span data-stu-id="779ab-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="779ab-432">Puede encontrar esta información en la sección [HDInsight con grupos de seguridad de red y rutas definidas por el usuario](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="779ab-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="779ab-433">En este ejemplo se muestra cómo agregar reglas para permitir el tráfico de entrada en las direcciones IP necesarias.</span><span class="sxs-lookup"><span data-stu-id="779ab-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="779ab-434">No contiene una regla para restringir el acceso de entrada desde otros orígenes.</span><span class="sxs-lookup"><span data-stu-id="779ab-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="779ab-435">En el siguiente ejemplo se muestra cómo habilitar el acceso de SSH desde Internet:</span><span class="sxs-lookup"><span data-stu-id="779ab-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="779ab-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="779ab-436">Azure CLI</span></span>

<span data-ttu-id="779ab-437">Use los pasos siguientes para crear una red virtual que restringe el tráfico de entrada pero permite el tráfico desde las direcciones IP requeridas por HDInsight.</span><span class="sxs-lookup"><span data-stu-id="779ab-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="779ab-438">Use el siguiente comando para crear un nuevo grupo de seguridad de red denominado " `hdisecure`".</span><span class="sxs-lookup"><span data-stu-id="779ab-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="779ab-439">Reemplace **RESOURCEGROUPNAME** por el grupo de recursos que contiene la red de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="779ab-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="779ab-440">Reemplace **LOCATION** por la ubicación (región) en la que se haya creado el grupo.</span><span class="sxs-lookup"><span data-stu-id="779ab-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="779ab-441">Cuando se haya creado el grupo, recibirá información sobre el nuevo grupo.</span><span class="sxs-lookup"><span data-stu-id="779ab-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="779ab-442">Utilice lo siguiente para agregar reglas al nuevo grupo de seguridad de red que permitan la comunicación entrante en el puerto 443 desde el servicio de mantenimiento y administración de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="779ab-443">Reemplace **RESOURCEGROUPNAME** por el nombre del grupo de recursos que contiene la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="779ab-444">Cambie las direcciones IP que se usan en este ejemplo para que coincidan con la región de Azure que está usando.</span><span class="sxs-lookup"><span data-stu-id="779ab-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="779ab-445">Puede encontrar esta información en la sección [HDInsight con grupos de seguridad de red y rutas definidas por el usuario](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="779ab-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="779ab-446">Para recuperar el identificador único para este grupo de seguridad de red, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="779ab-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="779ab-447">Este comando devuelve un valor similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="779ab-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="779ab-448">Utilice comillas dobles alrededor del identificador en el comando si no obtiene los resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="779ab-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="779ab-449">Use el siguiente comando para aplicar el grupo de seguridad de red a una subred.</span><span class="sxs-lookup"><span data-stu-id="779ab-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="779ab-450">Reemplace los valores de __GUID__ y __RESOURCEGROUPNAME__ por los que se devolvieron en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="779ab-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="779ab-451">Reemplace __NOMBRE_RED_VIRTUAL__ y __NOMBRE_SUBRED__ por el nombre de red virtual y el de subred que quiere crear.</span><span class="sxs-lookup"><span data-stu-id="779ab-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="779ab-452">Una vez completado este comando, puede instalar HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="779ab-453">Con estos pasos solo se abre el acceso al servicio de mantenimiento y administración de HDInsight en Azure Cloud.</span><span class="sxs-lookup"><span data-stu-id="779ab-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="779ab-454">Cualquier otro acceso al clúster de HDInsight desde fuera de Virtual Network está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="779ab-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="779ab-455">Para permitir el acceso desde fuera de la red virtual, debe agregar reglas adicionales del grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="779ab-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="779ab-456">En el siguiente ejemplo se muestra cómo habilitar el acceso de SSH desde Internet:</span><span class="sxs-lookup"><span data-stu-id="779ab-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="779ab-457"><a id="example-dns"></a> Ejemplo: configuración de DNS</span><span class="sxs-lookup"><span data-stu-id="779ab-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="779ab-458">Resolución de nombres entre una red virtual y una red local conectada</span><span class="sxs-lookup"><span data-stu-id="779ab-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="779ab-459">En este ejemplo se da por supuesto lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="779ab-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="779ab-460">Dispone de una instancia de Azure Virtual Network que está conectada a una red local mediante una puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="779ab-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="779ab-461">El servidor DNS personalizado en la red virtual ejecuta Linux o Unix como sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="779ab-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="779ab-462">[Bind](https://www.isc.org/downloads/bind/) está instalado en el servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="779ab-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="779ab-463">En el servidor DNS en la red virtual:</span><span class="sxs-lookup"><span data-stu-id="779ab-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="779ab-464">Use Azure PowerShell o la CLI de Azure para encontrar el sufijo DNS de la red virtual:</span><span class="sxs-lookup"><span data-stu-id="779ab-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="779ab-465">En el servidor DNS personalizado para la red virtual, use el siguiente texto como el contenido del archivo `/etc/bind/named.conf.local`:</span><span class="sxs-lookup"><span data-stu-id="779ab-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="779ab-466">Reemplace el valor `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` con el sufijo DNS de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="779ab-467">Esta configuración dirige todas las solicitudes DNS para el sufijo DNS de la red virtual a la resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="779ab-468">En el servidor DNS personalizado para la red virtual, use el siguiente texto como el contenido del archivo `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="779ab-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="779ab-469">Reemplace el valor `10.0.0.0/16` con el intervalo de direcciones IP de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="779ab-470">Esta entrada permite direcciones de solicitudes de resolución de nombres dentro de este intervalo.</span><span class="sxs-lookup"><span data-stu-id="779ab-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="779ab-471">Agregue el intervalo de direcciones IP de la red local a la sección `acl goodclients { ... }`.</span><span class="sxs-lookup"><span data-stu-id="779ab-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="779ab-472">Esta entrada permite las solicitudes de resolución de nombres de recursos de la red local.</span><span class="sxs-lookup"><span data-stu-id="779ab-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="779ab-473">Reemplace el valor `192.168.0.1` por la dirección IP del servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="779ab-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="779ab-474">Esta entrada enruta todas las solicitudes DNS al servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="779ab-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="779ab-475">Para usar la configuración, reinicie Bind.</span><span class="sxs-lookup"><span data-stu-id="779ab-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="779ab-476">Por ejemplo: `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="779ab-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="779ab-477">Agregue un reenviador condicional al servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="779ab-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="779ab-478">Configure el reenviador condicional para poder enviar solicitudes para el sufijo DNS del paso 1 al servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="779ab-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="779ab-479">Consulte la documentación del software de DNS para obtener información específica sobre cómo agregar un reenviador condicional.</span><span class="sxs-lookup"><span data-stu-id="779ab-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="779ab-480">Después de completar estos pasos, puede conectarse a los recursos de cualquiera de las redes mediante nombres de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="779ab-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="779ab-481">Ahora puede instalar HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="779ab-482">Resolución de nombres entre dos redes virtuales conectadas</span><span class="sxs-lookup"><span data-stu-id="779ab-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="779ab-483">En este ejemplo se da por supuesto lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="779ab-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="779ab-484">Tiene dos instancias de Azure Virtual Network que se conectan mediante una puerta de enlace de VPN o un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="779ab-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="779ab-485">El servidor DNS personalizado en ambas redes ejecuta Linux o Unix como sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="779ab-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="779ab-486">[Bind](https://www.isc.org/downloads/bind/) está instalado en los servidores DNS personalizados.</span><span class="sxs-lookup"><span data-stu-id="779ab-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="779ab-487">Use Azure PowerShell o la CLI de Azure para buscar el sufijo DNS de las dos redes virtuales:</span><span class="sxs-lookup"><span data-stu-id="779ab-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="779ab-488">Use el siguiente texto como contenido del archivo `/etc/bind/named.config.local` en el servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="779ab-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="779ab-489">Realice el cambio en el servidor DNS personalizado de las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="779ab-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="779ab-490">Reemplace el valor `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` con el sufijo DNS de la __otra__ red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="779ab-491">Esta entrada enruta las solicitudes para el sufijo DNS de la red remota al DNS personalizado en esa red.</span><span class="sxs-lookup"><span data-stu-id="779ab-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="779ab-492">En los servidores DNS personalizados de las dos redes virtuales, use el siguiente texto como contenido del archivo `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="779ab-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="779ab-493">Reemplace los valores `10.0.0.0/16` y `10.1.0.0/16` con el intervalo de direcciones IP de las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="779ab-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="779ab-494">Esta entrada permite que los recursos de cada red realicen solicitudes de los servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="779ab-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="779ab-495">Cualquier solicitud que no sea para los sufijos DNS de las redes virtuales (por ejemplo, microsoft.com) se administra mediante la resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="779ab-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="779ab-496">Para usar la configuración, reinicie Bind.</span><span class="sxs-lookup"><span data-stu-id="779ab-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="779ab-497">Por ejemplo, `sudo service bind9 restart` en ambos servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="779ab-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="779ab-498">Después de completar estos pasos, puede conectarse a recursos en la red virtual mediante nombres de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="779ab-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="779ab-499">Ahora puede instalar HDInsight en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="779ab-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="779ab-500">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="779ab-500">Next steps</span></span>

* <span data-ttu-id="779ab-501">Para obtener un ejemplo integral de la configuración de HDInsight para conectarse a una red local, vea [Conexión de HDInsight a la red local](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="779ab-502">Para más información sobre las redes virtuales de Azure, vea la [información general sobre Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="779ab-503">Para más información sobre los grupos de seguridad de red, vea [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="779ab-504">Para más información sobre las rutas definidas por el usuario, vea [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="779ab-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>