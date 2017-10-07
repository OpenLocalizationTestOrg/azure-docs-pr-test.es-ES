---
title: aaaConfigure un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure | Documentos de Microsoft
description: "Este tutorial usa recursos creados con el modelo de implementación clásica de Hola y crea una escucha del grupo de disponibilidad AlwaysOn en Azure que usa un equilibrador de carga interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="794b7-103">Configuración de un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure</span><span class="sxs-lookup"><span data-stu-id="794b7-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="794b7-104">Agente de escucha interno</span><span class="sxs-lookup"><span data-stu-id="794b7-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="794b7-105">Agente de escucha externo</span><span class="sxs-lookup"><span data-stu-id="794b7-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="794b7-106">Información general</span><span class="sxs-lookup"><span data-stu-id="794b7-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="794b7-107">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="794b7-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="794b7-108">Este artículo explica uso de Hola Hola clásico de modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="794b7-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="794b7-109">Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas.</span><span class="sxs-lookup"><span data-stu-id="794b7-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="794b7-110">tooconfigure un agente de escucha para un grupo de disponibilidad AlwaysOn en el modelo del Administrador de recursos de hello, consulte [configurar un equilibrador de carga para un grupo de disponibilidad AlwaysOn en Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="794b7-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="794b7-111">El grupo de disponibilidad puede contener réplicas que son solo locales, solo de Azure o abarcan ambas, locales y de Azure, para configuraciones híbridas.</span><span class="sxs-lookup"><span data-stu-id="794b7-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="794b7-112">Réplicas de Azure pueden residir en hello misma región o en varias regiones que utilizan varias redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="794b7-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="794b7-113">Hello procedimientos de este artículo se supone que ya ha [configurado un grupo de disponibilidad](../classic/portal-sql-alwayson-availability-groups.md) pero aún no ha configurado un agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="794b7-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="794b7-114">Instrucciones y limitaciones de los agentes de escucha internos</span><span class="sxs-lookup"><span data-stu-id="794b7-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="794b7-115">uso de Hola de un equilibrador de carga interno (ILB) con un agente de escucha del grupo de disponibilidad en Azure es toohello asunto siguientes instrucciones:</span><span class="sxs-lookup"><span data-stu-id="794b7-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="794b7-116">agente de escucha del grupo de disponibilidad de Hola se admite en Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="794b7-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="794b7-117">Sólo un agente de escucha del grupo de disponibilidad interna es compatible con los servicios de nube, porque el agente de escucha de hello es configurado toohello ILB, y no hay solo un ILB para cada servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="794b7-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="794b7-118">Sin embargo, es posible toocreate varios agentes de escucha externos.</span><span class="sxs-lookup"><span data-stu-id="794b7-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="794b7-119">Para más información, consulte [Configuración de un agente de escucha externo para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="794b7-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="794b7-120">Determinar la accesibilidad de Hola de agente de escucha de Hola</span><span class="sxs-lookup"><span data-stu-id="794b7-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="794b7-121">Este artículo se centra en la creación de un agente de escucha que usa un ILB.</span><span class="sxs-lookup"><span data-stu-id="794b7-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="794b7-122">Si necesita un agente de escucha público o externo, busque la versión de Hola de este artículo que se describe la configuración de un [agente de escucha externo](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="794b7-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="794b7-123">Creación de extremos de máquina virtual de carga equilibrada con Direct Server Return</span><span class="sxs-lookup"><span data-stu-id="794b7-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="794b7-124">Primero cree un ILB ejecutando script de Hola más adelante en esta sección.</span><span class="sxs-lookup"><span data-stu-id="794b7-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="794b7-125">Cree un punto de conexión de carga equilibrada para cada máquina virtual que hospeda una réplica de Azure.</span><span class="sxs-lookup"><span data-stu-id="794b7-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="794b7-126">Si tiene réplicas en varias regiones, cada réplica para esa región debe estar en el mismo servicio en la nube de Hola Hola misma red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="794b7-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="794b7-127">La creación de réplicas de grupo de disponibilidad que abarcan varias regiones de Azure requiere configurar varias redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="794b7-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="794b7-128">Para obtener más información acerca de cómo configurar cross conectividad de red virtual, vea [configurar la conectividad de red de red virtual toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="794b7-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="794b7-129">Hola portal de Azure, vaya tooeach máquina virtual que hospeda un detalles de réplica tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="794b7-130">Haga clic en hello **extremos** pestaña para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="794b7-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="794b7-131">Compruebe que hello **nombre** y **puerto público** de punto de conexión de agente de escucha de Hola que desea toouse no están ya en uso.</span><span class="sxs-lookup"><span data-stu-id="794b7-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="794b7-132">En el ejemplo de Hola en esta sección, se denomina hello *Miextremo*, y el puerto de hello es *1433*.</span><span class="sxs-lookup"><span data-stu-id="794b7-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="794b7-133">En el equipo local, descargue e instale hello más reciente [módulo de PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="794b7-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="794b7-134">Inicie Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="794b7-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="794b7-135">Se abre una nueva sesión de PowerShell, con hello Azure administrativos módulos cargados.</span><span class="sxs-lookup"><span data-stu-id="794b7-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="794b7-136">Ejecute `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="794b7-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="794b7-137">Este cmdlet le dirigirá toodownload de explorador tooa un directorio local tooa del archivo de publicar la configuración.</span><span class="sxs-lookup"><span data-stu-id="794b7-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="794b7-138">Puede que tenga que escribir las credenciales de inicio de sesión de la suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="794b7-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="794b7-139">Ejecute hello siguiente `Import-AzurePublishSettingsFile` comando con la ruta de acceso de Hola de hello publicar el archivo de configuración que ha descargado:</span><span class="sxs-lookup"><span data-stu-id="794b7-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="794b7-140">Después de publicar Hola se importa el archivo de configuración, puede administrar su suscripción de Azure en la sesión de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="794b7-141">En el *ILB*, asigne una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="794b7-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="794b7-142">Examine la configuración de red virtual actual de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="794b7-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="794b7-143">Hola Nota *subred* nombre de subred de Hola que contiene máquinas virtuales de Hola que hospedan réplicas de Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="794b7-144">Este nombre se usa en el parámetro hello $SubnetName en script de Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="794b7-145">Hola Nota *VirtualNetworkSite* asigne un nombre y Hola a partir de *AddressPrefix* de subred de Hola que contiene máquinas virtuales de Hola que hospedan réplicas de Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="794b7-146">Buscar una dirección IP disponible pasando ambos valores toohello `Test-AzureStaticVNetIP` comando y examinando hello *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="794b7-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="794b7-147">Por ejemplo, si hello red virtual se denomina *MyVNet* y tiene un intervalo de direcciones de subred que empieza a *172.16.0.128*, siguiente Hola comando haría una lista de direcciones disponibles:</span><span class="sxs-lookup"><span data-stu-id="794b7-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="794b7-148">Seleccione una de las direcciones disponibles de Hola y usarlo en el parámetro hello $ILBStaticIP del script de hello en el paso siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="794b7-149">Copie Hola después de editor de texto de tooa de secuencia de comandos de PowerShell y configure toosuit de valores de las variables de hello su entorno.</span><span class="sxs-lookup"><span data-stu-id="794b7-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="794b7-150">Se han proporcionado los valores predeterminados de algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="794b7-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="794b7-151">Las implementaciones existentes que usan grupos de afinidad no pueden agregar un ILB.</span><span class="sxs-lookup"><span data-stu-id="794b7-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="794b7-152">Para más información sobre requisitos de ILB, consulte [Información general sobre el equilibrador de carga interno](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="794b7-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="794b7-153">Además, si el grupo de disponibilidad abarca las regiones de Azure, debe ejecutar el script de Hola de una vez en cada centro de datos para el servicio de nube de Hola y nodos que residen en ese centro de datos.</span><span class="sxs-lookup"><span data-stu-id="794b7-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="794b7-154">Después de configurar las variables de hello, Hola copia escribirlo de hello texto editor tooyour PowerShell sesión toorun.</span><span class="sxs-lookup"><span data-stu-id="794b7-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="794b7-155">Si el mensaje de Hola sigue mostrando  **>>** , presione ENTRAR de nuevo que la secuencia de comandos de hello toomake empieza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="794b7-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="794b7-156">Comprobación de que KB2854082 está instalado si es necesario.</span><span class="sxs-lookup"><span data-stu-id="794b7-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="794b7-157">Abrir los puertos de firewall de hello en los nodos de grupo de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="794b7-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="794b7-158">Crear Agente de escucha del grupo de disponibilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="794b7-158">Create hello availability group listener</span></span>

<span data-ttu-id="794b7-159">Crear Agente de escucha del grupo de disponibilidad de hello en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="794b7-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="794b7-160">En primer lugar, cree el recurso de clúster de punto de acceso de cliente de Hola y configure las dependencias.</span><span class="sxs-lookup"><span data-stu-id="794b7-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="794b7-161">En segundo lugar, configure los recursos de clúster de hello en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="794b7-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="794b7-162">Crear punto de acceso de cliente de Hola y configurar las dependencias de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="794b7-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="794b7-163">Configurar los recursos de clúster de hello en PowerShell</span><span class="sxs-lookup"><span data-stu-id="794b7-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="794b7-164">Para el ILB, debe usar la dirección IP de Hola de hello ILB que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="794b7-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="794b7-165">tooobtain esta dirección IP de direcciones en PowerShell, Hola de uso siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="794b7-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="794b7-166">En una de las máquinas virtuales de hello, copie el script de PowerShell de hello para el editor de texto tooa de sistema operativo y, a continuación, establezca las variables de hello toohello los valores que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="794b7-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="794b7-167">Para Windows Server 2012 o posterior, use Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="794b7-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="794b7-168">Para Windows Server 2008 R2, utilice Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="794b7-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="794b7-169">Una vez que las variables de hello establecidas, abra una ventana de Windows PowerShell con privilegios elevados, pegar Hola escribirlo desde el editor de texto hello en su toorun de sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="794b7-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="794b7-170">Si el mensaje de Hola sigue mostrando  **>>** , presione ENTRAR nuevo toomake seguro de que el script de Hola empieza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="794b7-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="794b7-171">Repita los pasos anteriores para cada máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="794b7-172">Este script configura el recurso de dirección IP de hello con la dirección IP de hello del servicio de nube de Hola y configura otros parámetros, como puerto de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="794b7-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="794b7-173">Cuando se conecta el recurso de dirección IP hello, puede responder toohello sondeo en el puerto de sondeo de Hola de extremo con equilibrio de carga de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="794b7-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="794b7-174">Ponga Hola el agente de escucha en línea</span><span class="sxs-lookup"><span data-stu-id="794b7-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="794b7-175">Elementos de seguimiento</span><span class="sxs-lookup"><span data-stu-id="794b7-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="794b7-176">Agente de escucha de grupo de disponibilidad de prueba hello (dentro Hola misma red virtual)</span><span class="sxs-lookup"><span data-stu-id="794b7-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="794b7-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="794b7-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
