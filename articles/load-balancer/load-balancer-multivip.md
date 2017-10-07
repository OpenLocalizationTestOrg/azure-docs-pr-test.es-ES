---
title: aaaMutiple VIP para un servicio de nube
description: "Información general de varias VIP y cómo tooset varias VIP en un servicio de nube"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="dd43f-103">Configuración de varias direcciones VIP para un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="dd43f-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="dd43f-104">Puede tener acceso a los servicios de nube de Azure a través de hello Internet pública mediante una dirección IP proporcionada por Azure.</span><span class="sxs-lookup"><span data-stu-id="dd43f-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="dd43f-105">Esta dirección IP pública es tooas que se hace referencia una VIP (IP virtual) desde que se vinculó toohello Azure equilibrador de carga y no Hola instancias de máquina Virtual (VM) Hola del servicio en nube.</span><span class="sxs-lookup"><span data-stu-id="dd43f-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="dd43f-106">Con una sola dirección VIP puede tener acceso a cualquier instancia de máquina virtual dentro de un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="dd43f-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="dd43f-107">Sin embargo, hay escenarios en los que puede que necesite más de una VIP como un toohello de punto de entrada mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="dd43f-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="dd43f-108">Por ejemplo, el servicio de nube puede hospedar varios sitios Web que requieren conectividad SSL utiliza Hola puerto predeterminado 443, tal y como se hospeda cada sitio para un cliente diferente, o de inquilino.</span><span class="sxs-lookup"><span data-stu-id="dd43f-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="dd43f-109">En este escenario, debe toohave una dirección IP pública con orientación diferente para cada sitio Web.</span><span class="sxs-lookup"><span data-stu-id="dd43f-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="dd43f-110">Hello diagrama siguiente ilustra un hospedaje web multiempresa típica con una necesidad SSL varios certificados en hello mismo puerto público.</span><span class="sxs-lookup"><span data-stu-id="dd43f-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Escenario SSL de varias direcciones VIP](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="dd43f-112">En el ejemplo de Hola anterior, todas las direcciones VIP uso Hola mismo puerto público (443) y el tráfico se tooone redirigida o más carga equilibrada de máquinas virtuales en un único puerto privado para la dirección IP interna de Hola de todos los sitios Web de Hola de hospedaje de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd43f-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="dd43f-113">Otra situación que requiera Hola uso Hola varias VIP hospeda varios agentes de escucha de grupo de disponibilidad de AlwaysOn de SQL en el mismo conjunto de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd43f-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="dd43f-114">VIP son dinámicas de forma predeterminada, lo que significa que puede cambiar Hola real dirección IP asignada toohello servicio en la nube con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="dd43f-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="dd43f-115">tooprevent que suceda, puede reservar a una VIP para el servicio.</span><span class="sxs-lookup"><span data-stu-id="dd43f-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="dd43f-116">toolearn más información acerca de la VIP reservada, consulte [IP pública reservada](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="dd43f-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dd43f-117">Consulte [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obtener información sobre los precios de las direcciones VIP y las direcciones IP reservadas.</span><span class="sxs-lookup"><span data-stu-id="dd43f-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="dd43f-118">Puede usar PowerShell tooverify hello VIP utilizada los servicios de nube, así como agregar y quitar a VIP, asociar un punto de conexión de tooan VIP y configurar Equilibrio de carga en una sola dirección VIP específica.</span><span class="sxs-lookup"><span data-stu-id="dd43f-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="dd43f-119">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="dd43f-119">Limitations</span></span>

<span data-ttu-id="dd43f-120">En este momento, la funcionalidad de varias VIP está limitado toohello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd43f-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="dd43f-121">**Solo IaaS**.</span><span class="sxs-lookup"><span data-stu-id="dd43f-121">**IaaS only**.</span></span> <span data-ttu-id="dd43f-122">Solo puede habilitar VIP múltiples en servicios en la nube que contengan máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="dd43f-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="dd43f-123">No puede usar VIP múltiples en escenarios de PaaS, con instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="dd43f-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="dd43f-124">**Solo PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="dd43f-124">**PowerShell only**.</span></span> <span data-ttu-id="dd43f-125">Los VIP múltiples solo se pueden administrar mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd43f-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="dd43f-126">Estas limitaciones son temporales y pueden cambiar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="dd43f-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="dd43f-127">Asegúrese de toorevisit seguro de esta página tooverify los cambios futuros.</span><span class="sxs-lookup"><span data-stu-id="dd43f-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="dd43f-128">¿Cómo tooadd una VIP tooa servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="dd43f-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="dd43f-129">servicio de tooyour tooadd una VIP, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="dd43f-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="dd43f-130">Este comando muestra un toohello similar resultado según muestra:</span><span class="sxs-lookup"><span data-stu-id="dd43f-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="dd43f-131">¿Cómo tooremove una VIP de un servicio de nube</span><span class="sxs-lookup"><span data-stu-id="dd43f-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="dd43f-132">Hola tooremove VIP agregados servicio tooyour en el ejemplo de Hola anteriormente, Hola ejecución siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd43f-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="dd43f-133">Sólo se puede quitar a una VIP si no tiene ningún tooit extremos asociados.</span><span class="sxs-lookup"><span data-stu-id="dd43f-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="dd43f-134">La información de tooretrieve VIP de un servicio de nube</span><span class="sxs-lookup"><span data-stu-id="dd43f-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="dd43f-135">Hola tooretrieve VIP asociada a un servicio en la nube, ejecute el siguiente script de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="dd43f-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="dd43f-136">script de Hola muestra un toohello similar resultado según muestra:</span><span class="sxs-lookup"><span data-stu-id="dd43f-136">hello script displays a result similar toohello following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="dd43f-137">En este ejemplo, el servicio de nube de hello tiene 3 VIP:</span><span class="sxs-lookup"><span data-stu-id="dd43f-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="dd43f-138">**Vip1** se Hola predeterminado VIP, sabrá que porque se establece el valor de Hola para IsDnsProgrammedName tootrue.</span><span class="sxs-lookup"><span data-stu-id="dd43f-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="dd43f-139">**Vip2** y **Vip3** no se usan, ya que no tienen ninguna dirección IP.</span><span class="sxs-lookup"><span data-stu-id="dd43f-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="dd43f-140">Sólo se utilizarán si asocia un toohello extremo VIP.</span><span class="sxs-lookup"><span data-stu-id="dd43f-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="dd43f-141">Solo se cobrarán las direcciones VIP adicionales de su suscripción una vez que estén asociadas a un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="dd43f-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="dd43f-142">Para obtener más información sobre los precios, consulte [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="dd43f-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="dd43f-143">¿Cómo tooassociate una VIP tooan extremo</span><span class="sxs-lookup"><span data-stu-id="dd43f-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="dd43f-144">tooassociate una VIP en un extremo de tooan de servicio de nube, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="dd43f-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="dd43f-145">comando Hello crea un extremo VIP toohello vinculado llamado *Vip2* en el puerto *80*y se proporcionan vínculos toohello máquina virtual denominada *myVM1* en un servicio de nube denominado * myService* con *TCP* en el puerto *8080*.</span><span class="sxs-lookup"><span data-stu-id="dd43f-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="dd43f-146">configuración de hello tooverify, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="dd43f-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="dd43f-147">salida de Hello tiene un aspecto similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dd43f-147">hello output looks similar toohello following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="dd43f-148">¿Cómo tooenable equilibrio de carga en una sola dirección VIP específica</span><span class="sxs-lookup"><span data-stu-id="dd43f-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="dd43f-149">Puede asociar una sola dirección VIP a varias máquinas virtuales con el fin de equilibrar la carga.</span><span class="sxs-lookup"><span data-stu-id="dd43f-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="dd43f-150">Por ejemplo, suponga que tiene un servicio en la nube denominado *myService* y dos máquinas virtuales denominadas *myVM1* y *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="dd43f-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="dd43f-151">Y el servicio en la nube tiene varias direcciones VIP, una de ellas denominada *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="dd43f-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="dd43f-152">Si desea que todo el tráfico tooport de tooensure *81* en *Vip2* se equilibra entre *myVM1* y *myVM2* en el puerto *8181 *, ejecute hello siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd43f-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="dd43f-153">También puede actualizar su toouse de equilibrador de carga una VIP diferente.</span><span class="sxs-lookup"><span data-stu-id="dd43f-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="dd43f-154">Por ejemplo, si ejecuta Hola comando de PowerShell a continuación, cambiará el conjunto toouse una VIP con el nombre de la Vip1 de equilibrio de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="dd43f-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="dd43f-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd43f-155">Next Steps</span></span>

[<span data-ttu-id="dd43f-156">Log Analytics para Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="dd43f-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="dd43f-157">Información general sobre el equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="dd43f-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="dd43f-158">Introducción al equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="dd43f-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="dd43f-159">Información general sobre redes virtuales</span><span class="sxs-lookup"><span data-stu-id="dd43f-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="dd43f-160">API de REST de IP reservada</span><span class="sxs-lookup"><span data-stu-id="dd43f-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
