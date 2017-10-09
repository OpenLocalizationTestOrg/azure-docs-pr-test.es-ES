---
title: "aaaCreate un interno de Azure carga equilibrador - PowerShell clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un interno cargar equilibrador de usar PowerShell en el modelo de implementación clásica de Hola"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="b8b7e-103">Primeros pasos en la creación de un equilibrador de carga interno (clásico) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8b7e-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8b7e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8b7e-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="b8b7e-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b8b7e-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="b8b7e-106">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b8b7e-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="b8b7e-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b8b7e-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b8b7e-108">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="b8b7e-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b8b7e-110">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b8b7e-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="b8b7e-111">Crear un equilibrador de carga interno establecido para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b8b7e-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="b8b7e-112">toocreate un equilibrador de carga interno establecido y Hola servidores que enviarán su tráfico tooit, tiene el mensaje de error toodo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="b8b7e-113">Cree una instancia de interno equilibrio de carga que será el punto de conexión de Hola de carga de toobe tráfico entrante están equilibrada en los servidores de Hola de un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="b8b7e-114">Agregue extremos correspondientes máquinas virtuales de toohello que va a recibir el tráfico entrante Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="b8b7e-115">Configure los servidores de Hola que van a enviar equilibrio de carga de hello tráfico toobe toosend su tráfico toohello dirección IP virtual (VIP) de instancia de equilibrio de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="b8b7e-116">Paso 1: crear una instancia de Equilibrio de carga interno</span><span class="sxs-lookup"><span data-stu-id="b8b7e-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="b8b7e-117">Para un servicio de nube existente o un servicio de nube implementado en una red virtual regional, puede crear una instancia de equilibrio de carga interno con hello después de comandos de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="b8b7e-118">Tenga en cuenta que este uso de hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) cmdlet de Windows PowerShell usa Hola de parámetros defaultprobe.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="b8b7e-119">Para obtener más información sobre conjuntos de parámetros adicionales, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8b7e-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="b8b7e-120">Paso 2: Agregar instancia del equilibrio de carga interno de toohello de puntos de conexión</span><span class="sxs-lookup"><span data-stu-id="b8b7e-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="b8b7e-121">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="b8b7e-122">Paso 3: Configurar su toosend servidores su extremo de equilibrio de carga interno nuevo de tráfico toohello</span><span class="sxs-lookup"><span data-stu-id="b8b7e-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="b8b7e-123">Demasiado ha configurar servidores de hello cuyo tráfico es continuo toobe con equilibrio de carga toouse Hola nueva dirección IP (Hola VIP) del programa Hola a instancia de equilibrio de carga interno.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="b8b7e-124">Se trata de una dirección de hello en qué Hola equilibrio de carga interno está escuchando la instancia.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="b8b7e-125">En la mayoría de los casos, deberá toojust agregar o modificar un registro DNS para hello VIP de instancia de equilibrio de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="b8b7e-126">Si especifica la dirección IP de Hola durante la creación de hello de instancia de equilibrio de carga interno de hello, ya tiene Hola VIP.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="b8b7e-127">En caso contrario, puede ver a Hola VIP de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="b8b7e-128">toouse estos comandos, rellene los valores de hello y quitar Hola < y >.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="b8b7e-129">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="b8b7e-130">En pantalla de Hola de hello comando Get-AzureInternalLoadBalancer, anote la dirección IP de Hola y que servidores de tooyour de cambios necesarios de Hola o tooensure de registros DNS que el tráfico se envía a toohello VIP estén.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="b8b7e-131">plataforma de Microsoft Azure de Hello usa una dirección IPv4 estática, enrutable públicamente para una amplia variedad de escenarios de administración.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="b8b7e-132">dirección IP de Hello es 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="b8b7e-133">Ningún firewall debe bloquear esta dirección IP, ya que puede causar un comportamiento inesperado.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="b8b7e-134">Con sentido tooAzure de equilibrio de carga interno, se usa esta dirección IP mediante la supervisión de sondeos de estado de mantenimiento de Hola de toodetermine equilibrador de carga de Hola para máquinas virtuales en un conjunto de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="b8b7e-135">Si un grupo de seguridad de red es toorestrict usado tráfico tooAzure máquinas en un conjunto de carga equilibrada internamente o aplicado tooa subred de red Virtual, asegúrese de que una regla de seguridad de red se agrega tráfico tooallow desde 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="b8b7e-136">Ejemplo de equilibrio de carga interno</span><span class="sxs-lookup"><span data-stu-id="b8b7e-136">Example of internal load balancing</span></span>

<span data-ttu-id="b8b7e-137">toostep le guía por hello final tooend proceso de creación de un conjunto de carga equilibrada para dos configuraciones de ejemplo, vea Hola siguientes secciones.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="b8b7e-138">Una aplicación de niveles múltiples accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="b8b7e-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="b8b7e-139">Desea tooprovide un servicio de base de datos con equilibrio de carga para un conjunto de servidores web de conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="b8b7e-140">Ambos conjuntos de servidores se hospedan en un solo servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="b8b7e-141">Puerto 1433 de la tooTCP de tráfico del servidor Web debe distribuirse entre las dos máquinas virtuales en el nivel de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="b8b7e-142">La figura 1 muestra la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-142">Figure 1 shows hello configuration.</span></span>

![Conjunto de equilibrio de carga interno para el nivel de base de datos de Hola](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="b8b7e-144">configuración de Hello consta de los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="b8b7e-145">servicio de Hello existente en la nube que hospeda máquinas virtuales de Hola se denomina mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="b8b7e-146">dos servidores de base de datos existente Hola se denominan DB1, DB2.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="b8b7e-147">Servidores Web en el nivel de web Hola conectan toohello servidores de base de datos en el nivel de base de datos de hello mediante el uso de direcciones IP privadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="b8b7e-148">Otra opción es toouse su propio DNS para la red virtual de Hola y registrar manualmente un registro a para el conjunto de equilibrador de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="b8b7e-149">Hello comandos siguientes configuran una nueva instancia de equilibrio de carga interno denominada **ILBset** y agregar máquinas virtuales extremos toohello que correspondiente toohello dos servidores de base de datos:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="b8b7e-150">Quitar una configuración de Equilibrio de carga interno</span><span class="sxs-lookup"><span data-stu-id="b8b7e-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="b8b7e-151">tooremove una máquina virtual como un punto de conexión de una instancia de equilibrador de carga interno, Hola de uso después de comandos:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="b8b7e-152">toouse estos comandos, rellene los valores de hello, quitar Hola < y >.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="b8b7e-153">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="b8b7e-154">tooremove una instancia de equilibrador de carga interno de un servicio de nube, Hola de uso siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="b8b7e-155">toouse estos comandos, complete el valor de Hola y quite Hola < y >.</span><span class="sxs-lookup"><span data-stu-id="b8b7e-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="b8b7e-156">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="b8b7e-157">Información adicional sobre los cmdlet de equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="b8b7e-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="b8b7e-158">tooobtain información adicional acerca de los cmdlets de equilibrio de carga interno, ejecute hello siga los comandos en un símbolo del sistema de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b8b7e-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="b8b7e-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8b7e-159">Next steps</span></span>

[<span data-ttu-id="b8b7e-160">Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen</span><span class="sxs-lookup"><span data-stu-id="b8b7e-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b8b7e-161">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="b8b7e-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

