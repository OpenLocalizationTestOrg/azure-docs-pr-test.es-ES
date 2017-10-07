---
title: equilibrador de carga de aaaConfigure de SQL AlwaysOn | Documentos de Microsoft
description: "Configurar toowork de equilibrador de carga con SQL siempre en y cómo tooleverage powershell toocreate equilibrador de carga para implementación de SQL de Hola"
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
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="938b5-103">Configuración del equilibrador de carga para SQL Always On</span><span class="sxs-lookup"><span data-stu-id="938b5-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="938b5-104">Los grupos de disponibilidad de SQL Server AlwaysOn se pueden ejecutar ahora con ILB.</span><span class="sxs-lookup"><span data-stu-id="938b5-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="938b5-105">El grupo de disponibilidad es la solución estrella de SQL Server para conseguir alta disponibilidad y recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="938b5-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="938b5-106">Hola agente de escucha del grupo de disponibilidad permite a las aplicaciones cliente tooseamlessly conectar la réplica principal de toohello, independientemente del número de Hola de réplicas de hello en la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="938b5-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="938b5-107">nombre de (dominio DNS) del agente de escucha de Hello es la dirección IP de tooa asignada con equilibrio de carga y equilibrador de carga de Azure indica el servidor principal de Hola entrantes tráfico tooonly Hola Hola conjunto de réplica.</span><span class="sxs-lookup"><span data-stu-id="938b5-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="938b5-108">Puede usar ILB para los extremos de SQL Server AlwaysOn (escucha).</span><span class="sxs-lookup"><span data-stu-id="938b5-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="938b5-109">Ahora tiene control sobre la accesibilidad de Hola de agente de escucha de Hola y elegir dirección IP con equilibrio de carga de Hola desde una subred específica de la red Virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="938b5-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="938b5-110">Mediante el uso de ILB en el agente de escucha de hello, Hola el punto de conexión SQL server (por ejemplo, Server = tcp:ListenerName, 1433; base de datos = DatabaseName) solo es accesible para:</span><span class="sxs-lookup"><span data-stu-id="938b5-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="938b5-111">Servicios y máquinas virtuales en Hola misma red Virtual</span><span class="sxs-lookup"><span data-stu-id="938b5-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="938b5-112">Servicios y máquinas virtuales de redes locales conectadas</span><span class="sxs-lookup"><span data-stu-id="938b5-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="938b5-113">Servicios y máquinas virtuales de redes virtuales interconectadas</span><span class="sxs-lookup"><span data-stu-id="938b5-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="938b5-115">Figura 1 - SQL AlwaysOn configurado con equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="938b5-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="938b5-116">Agregar servicio de toohello de equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="938b5-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="938b5-117">En el siguiente ejemplo de Hola, configuramos una red Virtual que contiene una subred llamada "Subred-1":</span><span class="sxs-lookup"><span data-stu-id="938b5-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="938b5-118">Agregue los extremos con equilibrio de carga para ILB en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="938b5-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="938b5-119">En el ejemplo de Hola anterior, tiene 2 VM llamado "sqlsvc1" y "sqlsvc2" ejecutar "Sqlsvc" del servicio en nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="938b5-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="938b5-120">Después de crear Hola ILB con `DirectServerReturn` cambiar, agregar extremos con equilibrio toohello ILB tooallow SQL tooconfigure Hola agentes de escucha para grupos de disponibilidad de Hola de carga.</span><span class="sxs-lookup"><span data-stu-id="938b5-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="938b5-121">Para más información sobre SQL AlwaysOn, consulte [Configuración de un equilibrador de carga interno para un grupo de disponibilidad AlwaysOn de Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="938b5-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="938b5-122">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="938b5-122">See Also</span></span>
[<span data-ttu-id="938b5-123">Introducción a la configuración de un equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="938b5-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="938b5-124">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="938b5-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="938b5-125">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="938b5-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="938b5-126">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="938b5-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
