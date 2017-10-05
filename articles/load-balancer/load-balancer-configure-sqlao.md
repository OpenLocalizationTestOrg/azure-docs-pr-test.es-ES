---
title: "Configuración de Load Balancer para SQL always on | Microsoft Docs"
description: "Configuración del equilibrador de carga para trabajar con SQL always on y cómo puede sacar provecho de powershell para crear el equilibrador de carga para la implementación de SQL"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 68aad6253f185d53fdd7f11c8660c7287ef12655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="01218-103">Configuración del equilibrador de carga para SQL Always On</span><span class="sxs-lookup"><span data-stu-id="01218-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="01218-104">Los grupos de disponibilidad de SQL Server AlwaysOn se pueden ejecutar ahora con ILB.</span><span class="sxs-lookup"><span data-stu-id="01218-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="01218-105">El grupo de disponibilidad es la solución estrella de SQL Server para conseguir alta disponibilidad y recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="01218-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="01218-106">El agente de escucha de grupo de disponibilidad permite a las aplicaciones cliente conectarse sin problemas a la réplica principal, independientemente del número de réplicas en la configuración.</span><span class="sxs-lookup"><span data-stu-id="01218-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="01218-107">El nombre (DNS) del agente de escucha está asignado a una dirección IP de carga equilibrada y el equilibrador de carga de Azure dirige el tráfico entrante únicamente al servidor principal del conjunto de réplicas.</span><span class="sxs-lookup"><span data-stu-id="01218-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="01218-108">Puede usar ILB para los extremos de SQL Server AlwaysOn (escucha).</span><span class="sxs-lookup"><span data-stu-id="01218-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="01218-109">Ahora tiene control sobre la accesibilidad del agente de escucha y puede elegir la dirección IP con equilibrio de carga de una subred específica de su red virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="01218-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="01218-110">Mediante el uso de ILB en el agente de escucha, solo pueden tener acceso al extremo del servidor SQL (por ejemplo, Server=tcp:ListenerName,1433;Database=DatabaseName):</span><span class="sxs-lookup"><span data-stu-id="01218-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="01218-111">Servicios y máquinas virtuales en la misma red virtual</span><span class="sxs-lookup"><span data-stu-id="01218-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="01218-112">Servicios y máquinas virtuales de redes locales conectadas</span><span class="sxs-lookup"><span data-stu-id="01218-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="01218-113">Servicios y máquinas virtuales de redes virtuales interconectadas</span><span class="sxs-lookup"><span data-stu-id="01218-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="01218-115">Figura 1 - SQL AlwaysOn configurado con equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="01218-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="01218-116">Agregar el equilibrador de carga interno al servicio</span><span class="sxs-lookup"><span data-stu-id="01218-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="01218-117">En el siguiente ejemplo, se configurará una red virtual que contiene una subred llamada "Subred-1":</span><span class="sxs-lookup"><span data-stu-id="01218-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="01218-118">Agregue los extremos con equilibrio de carga para ILB en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01218-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="01218-119">En el ejemplo anterior, tiene 2 máquinas virtuales llamadas "sqlsvc1" y "sqlsvc2" que se ejecutan en el servicio en la nube "Sqlsvc".</span><span class="sxs-lookup"><span data-stu-id="01218-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="01218-120">Después de crear el ILB con el conmutador `DirectServerReturn`, agregue los puntos de conexión de carga equilibrada al ILB para permitir que SQL configure los agentes de escucha para los grupos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="01218-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="01218-121">Para más información sobre SQL AlwaysOn, consulte [Configuración de un equilibrador de carga interno para un grupo de disponibilidad AlwaysOn de Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="01218-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="01218-122">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="01218-122">See Also</span></span>
[<span data-ttu-id="01218-123">Introducción a la configuración de un equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="01218-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="01218-124">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="01218-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="01218-125">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="01218-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="01218-126">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="01218-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
