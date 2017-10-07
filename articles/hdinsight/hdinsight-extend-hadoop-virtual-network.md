---
title: aaaExtend HDInsight con la red Virtual - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse red Virtual de Azure tooconnect HDInsight tooother nube recursos o los recursos de su centro de datos"
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
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="cd621-103">Extender Azure HDInsight mediante una instancia de Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="cd621-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="cd621-104">Obtenga información acerca de cómo toouse HDInsight con una [red Virtual de Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd621-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="cd621-105">El uso de una red Virtual de Azure permite Hola los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd621-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="cd621-106">Conexión tooHDInsight directamente desde una red local.</span><span class="sxs-lookup"><span data-stu-id="cd621-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="cd621-107">Conexión HDInsight toodata almacena en una red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="cd621-108">Directamente Hola a Hadoop acceso a los servicios que no están disponibles públicamente en internet.</span><span class="sxs-lookup"><span data-stu-id="cd621-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="cd621-109">Por ejemplo, las API de Kafka o hello API de Java de HBase.</span><span class="sxs-lookup"><span data-stu-id="cd621-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="cd621-110">información de Hello en este documento requiere una descripción de las redes TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="cd621-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="cd621-111">Si no está familiarizado con las redes TCP/IP, debe asociarse con alguien antes de efectuar modificaciones tooproduction redes.</span><span class="sxs-lookup"><span data-stu-id="cd621-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="cd621-112">Planificación</span><span class="sxs-lookup"><span data-stu-id="cd621-112">Planning</span></span>

<span data-ttu-id="cd621-113">siguiente Hola es preguntas de Hola que debe responder al planear tooinstall HDInsight en una red virtual:</span><span class="sxs-lookup"><span data-stu-id="cd621-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="cd621-114">¿Necesita tooinstall HDInsight en una red virtual existente?</span><span class="sxs-lookup"><span data-stu-id="cd621-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="cd621-115">¿O bien está creando una red nueva?</span><span class="sxs-lookup"><span data-stu-id="cd621-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="cd621-116">Si usa una red virtual existente, deberá toomodify configuración de red de hello antes de poder instalar HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="cd621-117">Para obtener más información, vea hello [agregar red virtual existente del tooan HDInsight](#existingvnet) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="cd621-118">¿Desea que contiene la red virtual de HDInsight tooanother red tooconnect Hola virtual o la red local?</span><span class="sxs-lookup"><span data-stu-id="cd621-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="cd621-119">trabajo de tooeasily con los recursos a través de redes, que puede necesita toocreate un DNS personalizado y configurar el reenvío de DNS.</span><span class="sxs-lookup"><span data-stu-id="cd621-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="cd621-120">Para obtener más información, vea hello [conectar varias redes](#multinet) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="cd621-121">¿Desea toorestrict/redirigir el tráfico entrante o saliente tooHDInsight?</span><span class="sxs-lookup"><span data-stu-id="cd621-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="cd621-122">HDInsight debe tiene ilimitado comunicación con direcciones IP específicas en el centro de datos de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="cd621-123">También hay varios puertos que deben permitirse a través de los firewalls para la comunicación del cliente.</span><span class="sxs-lookup"><span data-stu-id="cd621-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="cd621-124">Para obtener más información, vea hello [controlar el tráfico de red](#networktraffic) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="cd621-125"><a id="existingvnet"></a>Agregar la red virtual de HDInsight tooan existente</span><span class="sxs-lookup"><span data-stu-id="cd621-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="cd621-126">Usar pasos hello en esta sección toodiscover cómo tooadd un nuevo tooan de HDInsight existente de la red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="cd621-127">No se puede agregar un clúster de HDInsight existente a una red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="cd621-128">¿Está usando un clásico o el modelo de implementación del Administrador de recursos de red virtual de hello?</span><span class="sxs-lookup"><span data-stu-id="cd621-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="cd621-129">HDInsight 3.4 y versiones posteriores requieren una red virtual de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd621-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="cd621-130">Las versiones anteriores de HDInsight requieren una red virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="cd621-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="cd621-131">Si la red existente es una red virtual clásica, debe crear una red virtual del Administrador de recursos y, a continuación, conectarse Hola dos.</span><span class="sxs-lookup"><span data-stu-id="cd621-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="cd621-132">[Conectar toonew de redes virtuales clásica redes virtuales](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd621-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="cd621-133">Una vez admitido, HDInsight instalado en red de administrador de recursos de hello puede interactuar con los recursos de red clásicos Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="cd621-134">¿Usa tunelización forzada?</span><span class="sxs-lookup"><span data-stu-id="cd621-134">Do you use forced tunneling?</span></span> <span data-ttu-id="cd621-135">La tunelización forzada es una configuración de subred que fuerza la salida dispositivo tooa de tráfico de Internet para la inspección y el registro.</span><span class="sxs-lookup"><span data-stu-id="cd621-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="cd621-136">HDInsight no es compatible con la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="cd621-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="cd621-137">Quite la tunelización forzada antes de instalar HDInsight en una subred, o bien cree una nueva subred para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="cd621-138">¿Usa grupos de seguridad de red, las rutas definidas por el usuario o el tráfico de los dispositivos de red Virtual toorestrict dentro o fuera de la red virtual de hello?</span><span class="sxs-lookup"><span data-stu-id="cd621-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="cd621-139">Como un servicio administrado, HDInsight requiere un acceso sin restricciones tooseveral direcciones IP en el centro de datos de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="cd621-140">comunicación tooallow con estas direcciones IP, actualice las rutas definidas por el usuario ni grupos de seguridad de red existentes.</span><span class="sxs-lookup"><span data-stu-id="cd621-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="cd621-141">HDInsight hospeda varios servicios, que usan varios puertos.</span><span class="sxs-lookup"><span data-stu-id="cd621-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="cd621-142">No bloquee el tráfico de los puertos toothese.</span><span class="sxs-lookup"><span data-stu-id="cd621-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="cd621-143">Para obtener una lista de puertos tooallow a través de firewalls de dispositivo virtual, vea hello [seguridad](#security) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="cd621-144">toofind la configuración de seguridad existente, Hola de uso después de los comandos de Azure PowerShell o CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="cd621-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="cd621-145">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="cd621-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="cd621-146">Para obtener más información, vea hello [solucionar problemas de grupos de seguridad de red](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="cd621-147">Se aplican reglas de grupo de seguridad de red en orden según la prioridad de la regla.</span><span class="sxs-lookup"><span data-stu-id="cd621-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="cd621-148">se aplica Hola primera regla que coincide con el patrón de tráfico de hello y no hay otras se aplican para que el tráfico.</span><span class="sxs-lookup"><span data-stu-id="cd621-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="cd621-149">Reglas de orden de más permisivo tooleast permisivo.</span><span class="sxs-lookup"><span data-stu-id="cd621-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="cd621-150">Para obtener más información, vea hello [filtrar el tráfico de red con grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="cd621-151">Rutas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="cd621-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="cd621-152">Para obtener más información, vea hello [solucionar problemas de rutas](../virtual-network/virtual-network-routes-troubleshoot-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="cd621-153">Crear un clúster de HDInsight y seleccione Hola red Virtual de Azure durante la configuración.</span><span class="sxs-lookup"><span data-stu-id="cd621-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="cd621-154">Siga los pasos de Hola Hola siguiendo el proceso de creación de documentos toounderstand Hola clúster:</span><span class="sxs-lookup"><span data-stu-id="cd621-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="cd621-155">Crear HDInsight con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cd621-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="cd621-156">Creación de HDInsight con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd621-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="cd621-157">Creación de HDInsight con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="cd621-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="cd621-158">Creación de una instancia de HDInsight mediante el uso de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cd621-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="cd621-159">Agregar HDInsight tooa de red virtual es un paso de configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="cd621-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="cd621-160">Estar seguro de red virtual de tooselect Hola al configurar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="cd621-161"><a id="multinet"></a>Conectar varias redes</span><span class="sxs-lookup"><span data-stu-id="cd621-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="cd621-162">mayor desafío de Hello con una configuración de la red es la resolución de nombres entre redes de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="cd621-163">Azure proporciona resolución de nombres para los servicios de Azure instalados en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="cd621-164">Esta resolución de nombre integrado permite HDInsight tooconnect toohello después de recursos mediante un nombre de dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="cd621-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="cd621-165">Hola a cualquier recurso que está disponible en internet.</span><span class="sxs-lookup"><span data-stu-id="cd621-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="cd621-166">Por ejemplo, microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="cd621-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="cd621-167">Cualquier recurso que está en Hola misma red Virtual de Azure, mediante el uso de hello __nombre DNS interno__ del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="cd621-168">Por ejemplo, cuando se utiliza la resolución de nombres predeterminado de hello, siguiente Hola es nodos de ejemplo internos DNS nombres tooHDInsight asignado trabajo:</span><span class="sxs-lookup"><span data-stu-id="cd621-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="cd621-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="cd621-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="cd621-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="cd621-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="cd621-171">Estos dos nodos pueden comunicarse directamente entre sí y con otros nodos de HDInsight, mediante el uso de nombres DNS internos.</span><span class="sxs-lookup"><span data-stu-id="cd621-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="cd621-172">resolución de nombres predeterminado de Hello __no__ permitir HDInsight tooresolve nombres Hola de recursos en redes que están unidos a un toohello red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="cd621-173">Por ejemplo, es común toojoin toohello de red virtual de red local.</span><span class="sxs-lookup"><span data-stu-id="cd621-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="cd621-174">Con solo Hola predeterminada resolución de nombres, HDInsight no puede acceder a recursos de red local de Hola por su nombre.</span><span class="sxs-lookup"><span data-stu-id="cd621-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="cd621-175">Hola opuesto también es true, los recursos de la red local no pueden acceder a recursos de red virtual de Hola por su nombre.</span><span class="sxs-lookup"><span data-stu-id="cd621-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="cd621-176">Debe crear el servidor DNS personalizado de Hola y configurar hello toouse de red virtual, antes de crear Hola clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="cd621-177">resolución de nombres de tooenable entre la red virtual de Hola y recursos en redes combinadas, debe realizar Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="cd621-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="cd621-178">Crear un servidor DNS personalizado en hello donde piensa tooinstall HDInsight de red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="cd621-179">Configurar el servidor DNS personalizado de hello red virtual toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="cd621-180">Buscar hello que Azure asigna el sufijo DNS para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="cd621-181">Este valor es similar demasiado`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="cd621-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="cd621-182">Para obtener información acerca de la búsqueda de sufijo DNS de hello, vea hello [ejemplo: DNS personalizada](#example-dns) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="cd621-183">Configure el enrutamiento entre los servidores DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="cd621-184">configuración de Hello depende de tipo hello de red remota.</span><span class="sxs-lookup"><span data-stu-id="cd621-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="cd621-185">Si la red remota hello es una red local, configure el DNS como sigue:</span><span class="sxs-lookup"><span data-stu-id="cd621-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="cd621-186">__DNS personalizado__ (en la red virtual de hello):</span><span class="sxs-lookup"><span data-stu-id="cd621-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="cd621-187">Reenviar solicitudes para el sufijo DNS de Hola de resolución de Azure recursiva de toohello Hola red virtual (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="cd621-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="cd621-188">Azure administra las solicitudes de recursos de red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="cd621-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="cd621-189">Reenviar todos los otros servidores DNS de local de toohello solicitudes.</span><span class="sxs-lookup"><span data-stu-id="cd621-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="cd621-190">Hola local de DNS controla todas las demás solicitudes de resolución de nombre, incluso las solicitudes de recursos de internet, como Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="cd621-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="cd621-191">__DNS local__: reenvíe las solicitudes para hello red virtual DNS sufijo toohello servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="cd621-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="cd621-192">servidor DNS personalizado de Hello, a continuación, reenvía a toohello recursiva Azure resolución.</span><span class="sxs-lookup"><span data-stu-id="cd621-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="cd621-193">Este solicitudes de configuración de las rutas de acceso completa nombres de dominio que contienen el sufijo DNS de Hola Hola virtual toohello personalizado DNS del servidor de red.</span><span class="sxs-lookup"><span data-stu-id="cd621-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="cd621-194">Todas las demás solicitudes (incluso para las direcciones públicas de internet) se controlan mediante el servidor DNS de hello en local.</span><span class="sxs-lookup"><span data-stu-id="cd621-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="cd621-195">Si la red remota hello es otra red Virtual de Azure, configure DNS de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="cd621-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="cd621-196">__DNS personalizado__ (en cada red virtual):</span><span class="sxs-lookup"><span data-stu-id="cd621-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="cd621-197">Las solicitudes para el sufijo DNS de Hola de redes virtuales Hola se reenvían toohello los servidores DNS personalizados.</span><span class="sxs-lookup"><span data-stu-id="cd621-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="cd621-198">Hola DNS en cada red virtual es responsable de resolver recursos dentro de su red.</span><span class="sxs-lookup"><span data-stu-id="cd621-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="cd621-199">Reenviar otro de resolución de Azure recursiva toohello de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="cd621-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="cd621-200">resolución recursiva de Hello es responsable de resolver locales y recursos de internet.</span><span class="sxs-lookup"><span data-stu-id="cd621-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="cd621-201">servidor DNS de Hola para cada red reenvía las solicitudes toohello otro, según el sufijo DNS.</span><span class="sxs-lookup"><span data-stu-id="cd621-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="cd621-202">Otras solicitudes se resuelven mediante hello Azure recursiva solucionador.</span><span class="sxs-lookup"><span data-stu-id="cd621-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="cd621-203">Para obtener un ejemplo de cada configuración, vea hello [ejemplo: DNS personalizada](#example-dns) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="cd621-204">Para obtener más información, vea hello [resolución de nombres para las máquinas virtuales e instancias de rol](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="cd621-205">Conectar directamente tooHadoop services</span><span class="sxs-lookup"><span data-stu-id="cd621-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="cd621-206">Documentación mayoría en HDInsight se da por supuesto que tiene acceso toohello clúster sobre Hola internet.</span><span class="sxs-lookup"><span data-stu-id="cd621-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="cd621-207">Por ejemplo, que se puede conectar el clúster de toohello en https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="cd621-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="cd621-208">Esta dirección utiliza la puerta de enlace pública hello, que no está disponible si ha usado NSG u Hola a UDRs toorestrict acceso desde internet.</span><span class="sxs-lookup"><span data-stu-id="cd621-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="cd621-209">tooconnect tooAmbari y otras páginas web a través de la red virtual de hello, utilice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cd621-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="cd621-210">nombres de dominio completo interno hello toodiscover (FQDN) de nodos de clúster de HDInsight de hello, use uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="cd621-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

    <span data-ttu-id="cd621-211">En lista de Hola de nodos devueltos, busque Hola FQDN de Hola nodos principales y usar Hola FQDN tooconnect tooAmbari y otros servicios web.</span><span class="sxs-lookup"><span data-stu-id="cd621-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="cd621-212">Por ejemplo, utilice `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="cd621-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cd621-213">Algunos servicios hospedados en nodos principales Hola sólo están activas en un nodo a la vez.</span><span class="sxs-lookup"><span data-stu-id="cd621-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="cd621-214">Si intenta obtener acceso a un servicio en un nodo principal y devuelve un error 404, cambie toohello otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="cd621-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="cd621-215">nodo de hello toodetermine y el puerto que un servicio está disponible en, vea hello [puertos utilizados por los servicios de Hadoop en HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="cd621-216"><a id="networktraffic"></a> Control del tráfico de red</span><span class="sxs-lookup"><span data-stu-id="cd621-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="cd621-217">Tráfico de red en un redes virtuales de Azure puede controlarse mediante Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="cd621-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="cd621-218">**Grupos de seguridad de red** (NSG) le permiten red toohello de toofilter tráfico entrante y saliente.</span><span class="sxs-lookup"><span data-stu-id="cd621-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="cd621-219">Para obtener más información, vea hello [filtrar el tráfico de red con grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="cd621-220">HDInsight no admite la restricción de tráfico saliente.</span><span class="sxs-lookup"><span data-stu-id="cd621-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="cd621-221">**Las rutas definidas por el usuario** (UDR) definen cómo fluye el tráfico entre los recursos de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="cd621-222">Para obtener más información, vea hello [rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="cd621-223">**Red aparatos virtuales** replicar la funcionalidad de Hola de dispositivos como los enrutadores y firewalls.</span><span class="sxs-lookup"><span data-stu-id="cd621-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="cd621-224">Para obtener más información, vea hello [dispositivos de red](https://azure.microsoft.com/solutions/network-appliances) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="cd621-225">Como un servicio administrado, HDInsight requiere los servicios de administración y mantenimiento de tooAzure acceso sin restricciones en hello nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="cd621-226">Al usar NSG y UDR, debe asegurarse de que estos servicios pueden seguir comunicándose con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="cd621-227">HDInsight expone servicios en varios puertos.</span><span class="sxs-lookup"><span data-stu-id="cd621-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="cd621-228">Cuando se utiliza un servidor de seguridad de dispositivo virtual, debe permitir el tráfico en hello puertos utilizados para estos servicios.</span><span class="sxs-lookup"><span data-stu-id="cd621-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="cd621-229">Para obtener más información, vea la sección de hello [puertos necesarios].</span><span class="sxs-lookup"><span data-stu-id="cd621-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="cd621-230"><a id="hdinsight-ip"></a> HDInsight con grupos de seguridad de red y rutas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="cd621-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="cd621-231">Si planea usar **grupos de seguridad de red** o **rutas definidas por el usuario** toocontrol el tráfico de red, lleve a cabo Hola siguientes acciones antes de instalar HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cd621-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="cd621-232">Identificar Hola región de Azure que piensa toouse para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="cd621-233">Identificar las direcciones IP Hola requeridas HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="cd621-234">Para obtener más información, vea hello [direcciones IP requiere HDInsight](#hdinsight-ip) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="cd621-235">Crear o modificar grupos de seguridad de red de Hola o rutas definidas por el usuario para la subred de Hola que planea tooinstall HDInsight en.</span><span class="sxs-lookup"><span data-stu-id="cd621-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="cd621-236">__Grupos de seguridad de red__: permitir __entrada__ tráfico en el puerto __443__ desde direcciones IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="cd621-237">__Las rutas definidas por el usuario__: crear una ruta de dirección IP tooeach y establecer hello __tipo de salto siguiente__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="cd621-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="cd621-238">Para obtener más información sobre grupos de seguridad de red o rutas definidas por el usuario, vea Hola siguiente documentación:</span><span class="sxs-lookup"><span data-stu-id="cd621-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="cd621-239">Grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="cd621-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="cd621-240">Rutas definidas por el usuario</span><span class="sxs-lookup"><span data-stu-id="cd621-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="cd621-241">Tunelización forzada</span><span class="sxs-lookup"><span data-stu-id="cd621-241">Forced tunneling</span></span>

<span data-ttu-id="cd621-242">La tunelización forzada es una configuración de enrutamiento definidas por el usuario donde todo el tráfico de subred es específicas de tooa forzada de red o ubicación, por ejemplo, la red local.</span><span class="sxs-lookup"><span data-stu-id="cd621-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="cd621-243">HDInsight __no__ es compatible con la tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="cd621-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="cd621-244"><a id="hdinsight-ip"></a> Direcciones IP necesarias</span><span class="sxs-lookup"><span data-stu-id="cd621-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd621-245">Hola mantenimiento de Azure y los servicios de administración deben ser capaz de toocommunicate con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="cd621-246">Si utiliza grupos de seguridad de red o rutas definidas por el usuario, permitir el tráfico de hello direcciones IP para estos tooreach de servicios HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="cd621-247">Si no utiliza grupos de seguridad de red o el tráfico de toocontrol de rutas definidas por el usuario, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="cd621-248">Si utiliza grupos de seguridad de red o rutas definidas por el usuario, debe permitir el tráfico de hello mantenimiento de Azure y servicios de administración tooreach HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="cd621-249">Usar hello después de direcciones IP de Hola de toofind de pasos que deben permitirse:</span><span class="sxs-lookup"><span data-stu-id="cd621-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="cd621-250">Siempre debe permitir el tráfico de hello después de direcciones IP:</span><span class="sxs-lookup"><span data-stu-id="cd621-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="cd621-251">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="cd621-251">IP address</span></span> | <span data-ttu-id="cd621-252">Puerto permitido</span><span class="sxs-lookup"><span data-stu-id="cd621-252">Allowed port</span></span> | <span data-ttu-id="cd621-253">Dirección</span><span class="sxs-lookup"><span data-stu-id="cd621-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="cd621-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="cd621-254">168.61.49.99</span></span> | <span data-ttu-id="cd621-255">443</span><span class="sxs-lookup"><span data-stu-id="cd621-255">443</span></span> | <span data-ttu-id="cd621-256">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-256">Inbound</span></span> |
    | <span data-ttu-id="cd621-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="cd621-257">23.99.5.239</span></span> | <span data-ttu-id="cd621-258">443</span><span class="sxs-lookup"><span data-stu-id="cd621-258">443</span></span> | <span data-ttu-id="cd621-259">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-259">Inbound</span></span> |
    | <span data-ttu-id="cd621-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="cd621-260">168.61.48.131</span></span> | <span data-ttu-id="cd621-261">443</span><span class="sxs-lookup"><span data-stu-id="cd621-261">443</span></span> | <span data-ttu-id="cd621-262">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-262">Inbound</span></span> |
    | <span data-ttu-id="cd621-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="cd621-263">138.91.141.162</span></span> | <span data-ttu-id="cd621-264">443</span><span class="sxs-lookup"><span data-stu-id="cd621-264">443</span></span> | <span data-ttu-id="cd621-265">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-265">Inbound</span></span> |

2. <span data-ttu-id="cd621-266">A continuación, si el clúster de HDInsight está en uno de hello siguiendo las regiones, debe permitir el tráfico desde direcciones IP de hello enumerados para la región de hello:</span><span class="sxs-lookup"><span data-stu-id="cd621-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cd621-267">Si no aparece Hola región de Azure que está usando, use únicamente cuatro direcciones IP Hola del paso 1.</span><span class="sxs-lookup"><span data-stu-id="cd621-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="cd621-268">País</span><span class="sxs-lookup"><span data-stu-id="cd621-268">Country</span></span> | <span data-ttu-id="cd621-269">Region</span><span class="sxs-lookup"><span data-stu-id="cd621-269">Region</span></span> | <span data-ttu-id="cd621-270">Direcciones IP permitidas</span><span class="sxs-lookup"><span data-stu-id="cd621-270">Allowed IP addresses</span></span> | <span data-ttu-id="cd621-271">Puerto permitido</span><span class="sxs-lookup"><span data-stu-id="cd621-271">Allowed port</span></span> | <span data-ttu-id="cd621-272">Dirección</span><span class="sxs-lookup"><span data-stu-id="cd621-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="cd621-273">Asia</span><span class="sxs-lookup"><span data-stu-id="cd621-273">Asia</span></span> | <span data-ttu-id="cd621-274">Asia oriental</span><span class="sxs-lookup"><span data-stu-id="cd621-274">East Asia</span></span> | <span data-ttu-id="cd621-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="cd621-275">23.102.235.122</span></span></br><span data-ttu-id="cd621-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="cd621-276">52.175.38.134</span></span> | <span data-ttu-id="cd621-277">443</span><span class="sxs-lookup"><span data-stu-id="cd621-277">443</span></span> | <span data-ttu-id="cd621-278">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-279">Sudeste asiático</span><span class="sxs-lookup"><span data-stu-id="cd621-279">Southeast Asia</span></span> | <span data-ttu-id="cd621-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="cd621-280">13.76.245.160</span></span></br><span data-ttu-id="cd621-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="cd621-281">13.76.136.249</span></span> | <span data-ttu-id="cd621-282">443</span><span class="sxs-lookup"><span data-stu-id="cd621-282">443</span></span> | <span data-ttu-id="cd621-283">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-283">Inbound</span></span> |
    | <span data-ttu-id="cd621-284">Australia</span><span class="sxs-lookup"><span data-stu-id="cd621-284">Australia</span></span> | <span data-ttu-id="cd621-285">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="cd621-285">Australia East</span></span> | <span data-ttu-id="cd621-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="cd621-286">104.210.84.115</span></span></br><span data-ttu-id="cd621-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="cd621-287">13.75.152.195</span></span> | <span data-ttu-id="cd621-288">443</span><span class="sxs-lookup"><span data-stu-id="cd621-288">443</span></span> | <span data-ttu-id="cd621-289">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-290">Sudeste de Australia</span><span class="sxs-lookup"><span data-stu-id="cd621-290">Australia Southeast</span></span> | <span data-ttu-id="cd621-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="cd621-291">13.77.2.56</span></span></br><span data-ttu-id="cd621-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="cd621-292">13.77.2.94</span></span> | <span data-ttu-id="cd621-293">443</span><span class="sxs-lookup"><span data-stu-id="cd621-293">443</span></span> | <span data-ttu-id="cd621-294">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-294">Inbound</span></span> |
    | <span data-ttu-id="cd621-295">Brasil</span><span class="sxs-lookup"><span data-stu-id="cd621-295">Brazil</span></span> | <span data-ttu-id="cd621-296">Sur de Brasil</span><span class="sxs-lookup"><span data-stu-id="cd621-296">Brazil South</span></span> | <span data-ttu-id="cd621-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="cd621-297">191.235.84.104</span></span></br><span data-ttu-id="cd621-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="cd621-298">191.235.87.113</span></span> | <span data-ttu-id="cd621-299">443</span><span class="sxs-lookup"><span data-stu-id="cd621-299">443</span></span> | <span data-ttu-id="cd621-300">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-300">Inbound</span></span> |
    | <span data-ttu-id="cd621-301">Canadá</span><span class="sxs-lookup"><span data-stu-id="cd621-301">Canada</span></span> | <span data-ttu-id="cd621-302">Este de Canadá</span><span class="sxs-lookup"><span data-stu-id="cd621-302">Canada East</span></span> | <span data-ttu-id="cd621-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="cd621-303">52.229.127.96</span></span></br><span data-ttu-id="cd621-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="cd621-304">52.229.123.172</span></span> | <span data-ttu-id="cd621-305">443</span><span class="sxs-lookup"><span data-stu-id="cd621-305">443</span></span> | <span data-ttu-id="cd621-306">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-307">Centro de Canadá</span><span class="sxs-lookup"><span data-stu-id="cd621-307">Canada Central</span></span> | <span data-ttu-id="cd621-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="cd621-308">52.228.37.66</span></span></br><span data-ttu-id="cd621-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="cd621-309">52.228.45.222</span></span> | <span data-ttu-id="cd621-310">443</span><span class="sxs-lookup"><span data-stu-id="cd621-310">443</span></span> | <span data-ttu-id="cd621-311">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-311">Inbound</span></span> |
    | <span data-ttu-id="cd621-312">China</span><span class="sxs-lookup"><span data-stu-id="cd621-312">China</span></span> | <span data-ttu-id="cd621-313">Norte de China</span><span class="sxs-lookup"><span data-stu-id="cd621-313">China North</span></span> | <span data-ttu-id="cd621-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="cd621-314">42.159.96.170</span></span></br><span data-ttu-id="cd621-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="cd621-315">139.217.2.219</span></span> | <span data-ttu-id="cd621-316">443</span><span class="sxs-lookup"><span data-stu-id="cd621-316">443</span></span> | <span data-ttu-id="cd621-317">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-318">Este de China</span><span class="sxs-lookup"><span data-stu-id="cd621-318">China East</span></span> | <span data-ttu-id="cd621-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="cd621-319">42.159.198.178</span></span></br><span data-ttu-id="cd621-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="cd621-320">42.159.234.157</span></span> | <span data-ttu-id="cd621-321">443</span><span class="sxs-lookup"><span data-stu-id="cd621-321">443</span></span> | <span data-ttu-id="cd621-322">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-322">Inbound</span></span> |
    | <span data-ttu-id="cd621-323">Europa</span><span class="sxs-lookup"><span data-stu-id="cd621-323">Europe</span></span> | <span data-ttu-id="cd621-324">Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="cd621-324">North Europe</span></span> | <span data-ttu-id="cd621-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="cd621-325">52.164.210.96</span></span></br><span data-ttu-id="cd621-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="cd621-326">13.74.153.132</span></span> | <span data-ttu-id="cd621-327">443</span><span class="sxs-lookup"><span data-stu-id="cd621-327">443</span></span> | <span data-ttu-id="cd621-328">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-329">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="cd621-329">West Europe</span></span>| <span data-ttu-id="cd621-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="cd621-330">52.166.243.90</span></span></br><span data-ttu-id="cd621-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="cd621-331">52.174.36.244</span></span> | <span data-ttu-id="cd621-332">443</span><span class="sxs-lookup"><span data-stu-id="cd621-332">443</span></span> | <span data-ttu-id="cd621-333">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-333">Inbound</span></span> |
    | <span data-ttu-id="cd621-334">Alemania</span><span class="sxs-lookup"><span data-stu-id="cd621-334">Germany</span></span> | <span data-ttu-id="cd621-335">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="cd621-335">Germany Central</span></span> | <span data-ttu-id="cd621-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="cd621-336">51.4.146.68</span></span></br><span data-ttu-id="cd621-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="cd621-337">51.4.146.80</span></span> | <span data-ttu-id="cd621-338">443</span><span class="sxs-lookup"><span data-stu-id="cd621-338">443</span></span> | <span data-ttu-id="cd621-339">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-340">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="cd621-340">Germany Northeast</span></span> | <span data-ttu-id="cd621-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="cd621-341">51.5.150.132</span></span></br><span data-ttu-id="cd621-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="cd621-342">51.5.144.101</span></span> | <span data-ttu-id="cd621-343">443</span><span class="sxs-lookup"><span data-stu-id="cd621-343">443</span></span> | <span data-ttu-id="cd621-344">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-344">Inbound</span></span> |
    | <span data-ttu-id="cd621-345">India</span><span class="sxs-lookup"><span data-stu-id="cd621-345">India</span></span> | <span data-ttu-id="cd621-346">India Central</span><span class="sxs-lookup"><span data-stu-id="cd621-346">Central India</span></span> | <span data-ttu-id="cd621-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="cd621-347">52.172.153.209</span></span></br><span data-ttu-id="cd621-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="cd621-348">52.172.152.49</span></span> | <span data-ttu-id="cd621-349">443</span><span class="sxs-lookup"><span data-stu-id="cd621-349">443</span></span> | <span data-ttu-id="cd621-350">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-350">Inbound</span></span> |
    | <span data-ttu-id="cd621-351">Japón</span><span class="sxs-lookup"><span data-stu-id="cd621-351">Japan</span></span> | <span data-ttu-id="cd621-352">Este de Japón</span><span class="sxs-lookup"><span data-stu-id="cd621-352">Japan East</span></span> | <span data-ttu-id="cd621-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="cd621-353">13.78.125.90</span></span></br><span data-ttu-id="cd621-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="cd621-354">13.78.89.60</span></span> | <span data-ttu-id="cd621-355">443</span><span class="sxs-lookup"><span data-stu-id="cd621-355">443</span></span> | <span data-ttu-id="cd621-356">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-357">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="cd621-357">Japan West</span></span> | <span data-ttu-id="cd621-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="cd621-358">40.74.125.69</span></span></br><span data-ttu-id="cd621-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="cd621-359">138.91.29.150</span></span> | <span data-ttu-id="cd621-360">443</span><span class="sxs-lookup"><span data-stu-id="cd621-360">443</span></span> | <span data-ttu-id="cd621-361">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-361">Inbound</span></span> |
    | <span data-ttu-id="cd621-362">Corea</span><span class="sxs-lookup"><span data-stu-id="cd621-362">Korea</span></span> | <span data-ttu-id="cd621-363">Corea Central</span><span class="sxs-lookup"><span data-stu-id="cd621-363">Korea Central</span></span> | <span data-ttu-id="cd621-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="cd621-364">52.231.39.142</span></span></br><span data-ttu-id="cd621-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="cd621-365">52.231.36.209</span></span> | <span data-ttu-id="cd621-366">433</span><span class="sxs-lookup"><span data-stu-id="cd621-366">433</span></span> | <span data-ttu-id="cd621-367">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-368">Corea del Sur</span><span class="sxs-lookup"><span data-stu-id="cd621-368">Korea South</span></span> | <span data-ttu-id="cd621-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="cd621-369">52.231.203.16</span></span></br><span data-ttu-id="cd621-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="cd621-370">52.231.205.214</span></span> | <span data-ttu-id="cd621-371">443</span><span class="sxs-lookup"><span data-stu-id="cd621-371">443</span></span> | <span data-ttu-id="cd621-372">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-372">Inbound</span></span>
    | <span data-ttu-id="cd621-373">Reino Unido</span><span class="sxs-lookup"><span data-stu-id="cd621-373">United Kingdom</span></span> | <span data-ttu-id="cd621-374">Oeste de Reino Unido</span><span class="sxs-lookup"><span data-stu-id="cd621-374">UK West</span></span> | <span data-ttu-id="cd621-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="cd621-375">51.141.13.110</span></span></br><span data-ttu-id="cd621-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="cd621-376">51.141.7.20</span></span> | <span data-ttu-id="cd621-377">443</span><span class="sxs-lookup"><span data-stu-id="cd621-377">443</span></span> | <span data-ttu-id="cd621-378">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-379">Sur del Reino Unido 2</span><span class="sxs-lookup"><span data-stu-id="cd621-379">UK South</span></span> | <span data-ttu-id="cd621-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="cd621-380">51.140.47.39</span></span></br><span data-ttu-id="cd621-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="cd621-381">51.140.52.16</span></span> | <span data-ttu-id="cd621-382">443</span><span class="sxs-lookup"><span data-stu-id="cd621-382">443</span></span> | <span data-ttu-id="cd621-383">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-383">Inbound</span></span> |
    | <span data-ttu-id="cd621-384">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="cd621-384">United States</span></span> | <span data-ttu-id="cd621-385">Central EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="cd621-385">Central US</span></span> | <span data-ttu-id="cd621-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="cd621-386">13.67.223.215</span></span></br><span data-ttu-id="cd621-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="cd621-387">40.86.83.253</span></span> | <span data-ttu-id="cd621-388">443</span><span class="sxs-lookup"><span data-stu-id="cd621-388">443</span></span> | <span data-ttu-id="cd621-389">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-390">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="cd621-390">North Central US</span></span> | <span data-ttu-id="cd621-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="cd621-391">157.56.8.38</span></span></br><span data-ttu-id="cd621-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="cd621-392">157.55.213.99</span></span> | <span data-ttu-id="cd621-393">443</span><span class="sxs-lookup"><span data-stu-id="cd621-393">443</span></span> | <span data-ttu-id="cd621-394">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-395">Centro occidental de EE.UU.</span><span class="sxs-lookup"><span data-stu-id="cd621-395">West Central US</span></span> | <span data-ttu-id="cd621-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="cd621-396">52.161.23.15</span></span></br><span data-ttu-id="cd621-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="cd621-397">52.161.10.167</span></span> | <span data-ttu-id="cd621-398">443</span><span class="sxs-lookup"><span data-stu-id="cd621-398">443</span></span> | <span data-ttu-id="cd621-399">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="cd621-400">Oeste de EE. UU. 2</span><span class="sxs-lookup"><span data-stu-id="cd621-400">West US 2</span></span> | <span data-ttu-id="cd621-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="cd621-401">52.175.211.210</span></span></br><span data-ttu-id="cd621-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="cd621-402">52.175.222.222</span></span> | <span data-ttu-id="cd621-403">443</span><span class="sxs-lookup"><span data-stu-id="cd621-403">443</span></span> | <span data-ttu-id="cd621-404">Entrada</span><span class="sxs-lookup"><span data-stu-id="cd621-404">Inbound</span></span> |

    <span data-ttu-id="cd621-405">Para obtener información acerca de hello IP direcciones toouse para administración pública de Azure, vea hello [inteligencia de gobierno Azure + análisis](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="cd621-406">Si usa un servidor DNS personalizado con la red virtual, también debe permitir el acceso desde __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="cd621-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="cd621-407">Esta es la dirección de la resolución recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="cd621-408">Para obtener más información, vea hello [la resolución de nombres para máquinas virtuales y rol instancias](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="cd621-409">Para obtener más información, vea hello [controlar el tráfico de red](#networktraffic) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="cd621-410"><a id="hdinsight-ports"></a> Puertos necesarios</span><span class="sxs-lookup"><span data-stu-id="cd621-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="cd621-411">Si planea usar una red **firewall del dispositivo virtual** toosecure red virtual de hello, debe permitir el tráfico saliente en hello siguientes puertos:</span><span class="sxs-lookup"><span data-stu-id="cd621-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="cd621-412">53</span><span class="sxs-lookup"><span data-stu-id="cd621-412">53</span></span>
* <span data-ttu-id="cd621-413">443</span><span class="sxs-lookup"><span data-stu-id="cd621-413">443</span></span>
* <span data-ttu-id="cd621-414">1433</span><span class="sxs-lookup"><span data-stu-id="cd621-414">1433</span></span>
* <span data-ttu-id="cd621-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="cd621-415">11000-11999</span></span>
* <span data-ttu-id="cd621-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="cd621-416">14000-14999</span></span>

<span data-ttu-id="cd621-417">Para obtener una lista de puertos para servicios específicos, vea hello [puertos utilizados por los servicios de Hadoop en HDInsight](hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="cd621-418">Para obtener más información sobre las reglas de firewall para aparatos virtuales, vea hello [escenario de dispositivo virtual](../virtual-network/virtual-network-scenario-udr-gw-nva.md) documento.</span><span class="sxs-lookup"><span data-stu-id="cd621-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="cd621-419"><a id="hdinsight-nsg"></a>Ejemplo: grupos de seguridad de red con HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd621-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="cd621-420">ejemplos de Hello en esta sección muestra cómo el grupo de seguridad de red de toocreate reglas que permiten el toocommunicate de HDInsight con hello servicios de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="cd621-421">Antes de usar los ejemplos de hello, ajustar Hola IP direcciones toomatch hello las para hello región de Azure que está utilizando.</span><span class="sxs-lookup"><span data-stu-id="cd621-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="cd621-422">Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="cd621-423">Plantilla de administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="cd621-423">Azure Resource Management template</span></span>

<span data-ttu-id="cd621-424">Hello siguiente plantilla de administración de recursos crea una red virtual que restringe el tráfico entrante, pero permite el tráfico de direcciones IP de hello requerido HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="cd621-425">Esta plantilla crea también un clúster de HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="cd621-426">Implementar una instancia segura de Azure Virtual Network y un clúster de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd621-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="cd621-427">Cambiar las direcciones IP de hello usa este Hola de toomatch ejemplo región de Azure que está utilizando.</span><span class="sxs-lookup"><span data-stu-id="cd621-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="cd621-428">Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="cd621-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd621-429">Azure PowerShell</span></span>

<span data-ttu-id="cd621-430">Usar hello después toocreate de secuencia de comandos de PowerShell una red virtual que restringe el tráfico entrante y permite el tráfico desde Hola direcciones IP para la región de Europa del Norte Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd621-431">Cambiar las direcciones IP de hello usa este Hola de toomatch ejemplo región de Azure que está utilizando.</span><span class="sxs-lookup"><span data-stu-id="cd621-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="cd621-432">Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
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
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="cd621-433">En este ejemplo se muestra cómo tooadd reglas tooallow el tráfico en direcciones IP de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="cd621-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="cd621-434">No contiene una regla toorestrict acceso de otros orígenes de entrada.</span><span class="sxs-lookup"><span data-stu-id="cd621-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="cd621-435">Hola siguiente ejemplo muestra cómo tener acceso tooenable SSH de hello Internet:</span><span class="sxs-lookup"><span data-stu-id="cd621-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="cd621-436">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cd621-436">Azure CLI</span></span>

<span data-ttu-id="cd621-437">Usar hello siguiendo los pasos toocreate una red virtual que restringe el tráfico entrante, pero permite el tráfico de direcciones IP de hello requerido HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd621-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="cd621-438">Hola de uso después toocreate comando un nuevo grupo de seguridad de red denominado `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="cd621-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="cd621-439">Reemplace **RESOURCEGROUPNAME** con grupo de recursos de Hola que contiene Hola red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="cd621-440">Reemplace **ubicación** con ubicación hello (región) se creó ese grupo hello en.</span><span class="sxs-lookup"><span data-stu-id="cd621-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="cd621-441">Una vez que se ha creado el grupo de hello, recibirá información sobre el nuevo grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="cd621-442">Usar hello después tooadd reglas toohello nuevo grupo de seguridad red que permiten la comunicación entrante en el puerto 443 de hello servicio de mantenimiento y administración de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="cd621-443">Reemplace **RESOURCEGROUPNAME** con el nombre de Hola Hola del grupo de recursos que contiene Hola red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cd621-444">Cambiar las direcciones IP de hello usa este Hola de toomatch ejemplo región de Azure que está utilizando.</span><span class="sxs-lookup"><span data-stu-id="cd621-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="cd621-445">Puede encontrar esta información en hello [HDInsight con grupos de seguridad de red y las rutas definidas por el usuario](#hdinsight-ip) sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="cd621-446">tooretrieve Hola identificador único para este grupo de seguridad de red, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cd621-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="cd621-447">Este comando devuelve un toohello similar valor siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="cd621-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="cd621-448">Utilice comillas dobles alrededor de Id. en comando hello si no obtiene resultados Hola esperado.</span><span class="sxs-lookup"><span data-stu-id="cd621-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="cd621-449">Usar hello después de la subred de tooa del grupo de seguridad de comando tooapply Hola red.</span><span class="sxs-lookup"><span data-stu-id="cd621-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="cd621-450">Reemplace hello __GUID__ y __RESOURCEGROUPNAME__ valores con hello las devuelven desde el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="cd621-451">Reemplace __VNETNAME__ y __SUBNETNAME__ con nombre de red virtual de Hola y el nombre de subred que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="cd621-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="cd621-452">Una vez completado este comando, puede instalar HDInsight en hello red Virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd621-453">Estos pasos solo abren toohello HDInsight mantenimiento y administración de servicio de acceso a Hola nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="cd621-454">Cualquier otro acceso toohello clúster de HDInsight de hello exterior red Virtual está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="cd621-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="cd621-455">tooenable acceso de red virtual externa hello, debe agregar reglas de grupo de seguridad de red adicionales.</span><span class="sxs-lookup"><span data-stu-id="cd621-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="cd621-456">Hola siguiente ejemplo muestra cómo tener acceso tooenable SSH de hello Internet:</span><span class="sxs-lookup"><span data-stu-id="cd621-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="cd621-457"><a id="example-dns"></a> Ejemplo: configuración de DNS</span><span class="sxs-lookup"><span data-stu-id="cd621-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="cd621-458">Resolución de nombres entre una red virtual y una red local conectada</span><span class="sxs-lookup"><span data-stu-id="cd621-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="cd621-459">En este ejemplo realiza Hola siguientes supuestos:</span><span class="sxs-lookup"><span data-stu-id="cd621-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="cd621-460">Dispone de una red Virtual de Azure que es la red local de tooan conectados mediante una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="cd621-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="cd621-461">servidor DNS personalizado de Hello en red virtual de Hola ejecuta Linux o Unix como sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="cd621-462">[Enlazar](https://www.isc.org/downloads/bind/) está instalado en el servidor DNS personalizado Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="cd621-463">En servidor DNS personalizado de hello en la red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="cd621-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="cd621-464">Usar Azure PowerShell o CLI de Azure toofind Hola sufijo DNS de red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="cd621-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="cd621-465">En el servidor DNS personalizado de hello para la red virtual de hello, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.local` archivo:</span><span class="sxs-lookup"><span data-stu-id="cd621-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="cd621-466">Reemplace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor con el sufijo DNS de saludo de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="cd621-467">Esta configuración enruta todas las solicitudes DNS para el sufijo DNS de Hola de resolución de hello red virtual toohello recursiva de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd621-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="cd621-468">En el servidor DNS personalizado de hello para la red virtual de hello, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.options` archivo:</span><span class="sxs-lookup"><span data-stu-id="cd621-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="cd621-469">Reemplace hello `10.0.0.0/16` valor con el intervalo de direcciones IP de hello de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="cd621-470">Esta entrada permite direcciones de solicitudes de resolución de nombres dentro de este intervalo.</span><span class="sxs-lookup"><span data-stu-id="cd621-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="cd621-471">Agregar intervalo de direcciones IP de Hola de hello local red toohello `acl goodclients { ... }` sección.</span><span class="sxs-lookup"><span data-stu-id="cd621-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="cd621-472">entrada permite las solicitudes de resolución de nombres de los recursos de red local de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="cd621-473">Reemplace el valor de hello `192.168.0.1` con la dirección IP de saludo del servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="cd621-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="cd621-474">Esta entrada enruta todos los demás DNS solicitudes toohello en servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="cd621-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="cd621-475">configuración de hello toouse, reinicie el enlace.</span><span class="sxs-lookup"><span data-stu-id="cd621-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="cd621-476">Por ejemplo: `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="cd621-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="cd621-477">Agregar un servidor DNS de reenviador condicional toohello local.</span><span class="sxs-lookup"><span data-stu-id="cd621-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="cd621-478">Configurar solicitudes de toosend de reenviador condicional de hello para el sufijo DNS de Hola de servidor DNS de paso 1 toohello personalizado.</span><span class="sxs-lookup"><span data-stu-id="cd621-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cd621-479">Consulte la documentación de hello para el software DNS para obtener información específica acerca de cómo tooadd un reenviador condicional.</span><span class="sxs-lookup"><span data-stu-id="cd621-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="cd621-480">Después de completar estos pasos, puede conectarse tooresources en cualquier red mediante nombres de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="cd621-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="cd621-481">Ahora puede instalar HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="cd621-482">Resolución de nombres entre dos redes virtuales conectadas</span><span class="sxs-lookup"><span data-stu-id="cd621-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="cd621-483">En este ejemplo realiza Hola siguientes supuestos:</span><span class="sxs-lookup"><span data-stu-id="cd621-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="cd621-484">Tiene dos instancias de Azure Virtual Network que se conectan mediante una puerta de enlace de VPN o un emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="cd621-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="cd621-485">servidor DNS personalizado de Hello en ambas redes ejecuta Linux o Unix como sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="cd621-486">[Enlazar](https://www.isc.org/downloads/bind/) está instalado en los servidores DNS personalizados Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="cd621-487">Usar Azure PowerShell o CLI de Azure toofind Hola sufijo DNS de ambas redes virtuales:</span><span class="sxs-lookup"><span data-stu-id="cd621-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="cd621-488">Hola de uso después de texto como contenido de Hola de hello `/etc/bind/named.config.local` archivo en el servidor DNS personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="cd621-489">Realice este cambio en el servidor DNS personalizado de hello en ambas redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="cd621-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="cd621-490">Reemplace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor con el sufijo DNS de Hola de hello __otros__ red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd621-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="cd621-491">Esta entrada enruta las solicitudes para el sufijo DNS de Hola de hello red remota toohello DNS personalizado en esa red.</span><span class="sxs-lookup"><span data-stu-id="cd621-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="cd621-492">En servidores DNS personalizados de hello en ambas redes virtuales, usar hello después de texto como contenido de Hola de hello `/etc/bind/named.conf.options` archivo:</span><span class="sxs-lookup"><span data-stu-id="cd621-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
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

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="cd621-493">Reemplace hello `10.0.0.0/16` y `10.1.0.0/16` valores con la dirección IP de hello intervalos de las redes virtuales de direcciones.</span><span class="sxs-lookup"><span data-stu-id="cd621-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="cd621-494">Esta entrada permite a los recursos de cada red toomake solicitudes de los servidores DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="cd621-495">Resolución de hello Azure recursiva administra las solicitudes que no son para los sufijos DNS Hola de redes virtuales de hello (por ejemplo, microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cd621-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="cd621-496">configuración de hello toouse, reinicie el enlace.</span><span class="sxs-lookup"><span data-stu-id="cd621-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="cd621-497">Por ejemplo, `sudo service bind9 restart` en ambos servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="cd621-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="cd621-498">Después de completar estos pasos, puede conectarse tooresources en red virtual de hello con nombres de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="cd621-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="cd621-499">Ahora puede instalar HDInsight en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd621-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd621-500">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd621-500">Next steps</span></span>

* <span data-ttu-id="cd621-501">Para obtener un ejemplo de extremo a extremo de la configuración de red de HDInsight tooconnect tooan locales, consulte [red local de conectar HDInsight tooan](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="cd621-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="cd621-502">Para obtener más información sobre redes virtuales de Azure, vea hello [información general de la red Virtual de Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd621-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="cd621-503">Para más información sobre los grupos de seguridad de red, vea [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="cd621-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="cd621-504">Para más información sobre las rutas definidas por el usuario, vea [Rutas definidas por el usuario y reenvío IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd621-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>