---
title: Varias direcciones VIP para un servicio en la nube
description: "Información general sobre multiVIP y cómo establecer varias direcciones VIP en un servicio en la nube"
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
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="ed4f9-103">Configuración de varias direcciones VIP para un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="ed4f9-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="ed4f9-104">Puede tener acceso a los servicios en la nube de Azure a través de la Internet pública mediante una dirección IP proporcionada por Azure.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="ed4f9-105">Esta dirección IP pública se conoce como una dirección VIP (IP virtual) dado que está vinculada a Azure Load Balancer y no realmente a las instancias de máquina virtual dentro del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="ed4f9-106">Con una sola dirección VIP puede tener acceso a cualquier instancia de máquina virtual dentro de un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="ed4f9-107">Sin embargo, hay escenarios en los que puede que necesite más de una dirección VIP como punto de entrada al mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="ed4f9-108">Por ejemplo, el servicio en la nube podría hospedar varios sitios web que requieren conectividad SSL usando el puerto predeterminado de 443, y cada sitio hospedarse para un cliente o inquilino diferente.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="ed4f9-109">En este escenario, deberá tener una dirección IP accesible de forma pública diferente para cada sitio web.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="ed4f9-110">El siguiente diagrama muestra un hospedaje web multiempresa típico en el que se necesitan varios certificados SSL en el mismo puerto público.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Escenario SSL de varias direcciones VIP](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="ed4f9-112">En el escenario anterior, todas las direcciones VIP usan el mismo puerto público (443) y el tráfico se redirige a una o varias máquinas virtuales con equilibrio de carga en un único puerto privado, según la dirección IP interna del servicio en la nube que hospeda todos los sitios web.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="ed4f9-113">Otro escenario de uso de varias direcciones VIP es el hospedaje de varios agentes de escucha de grupo de disponibilidad SQL AlwaysOn en el mismo conjunto de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="ed4f9-114">Las direcciones VIP son dinámicas de forma predeterminada, lo que significa que la dirección IP real asignada al servicio en la nube puede cambiar con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="ed4f9-115">Para evitar que esto suceda, puede reservar una dirección VIP para su servicio.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="ed4f9-116">Para obtener más información sobre las direcciones VIP reservadas, consulte [IP pública reservada](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="ed4f9-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ed4f9-117">Consulte [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obtener información sobre los precios de las direcciones VIP y las direcciones IP reservadas.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="ed4f9-118">Puede usar PowerShell para comprobar las direcciones VIP usadas por los servicios en la nube, y también para agregar y quitar direcciones VIP, asociar una dirección VIP a un extremo y configurar el equilibrio de carga para una dirección VIP específica.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="ed4f9-119">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="ed4f9-119">Limitations</span></span>

<span data-ttu-id="ed4f9-120">En este momento, la funcionalidad de VIP múltiples se limita a los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="ed4f9-121">**Solo IaaS**.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-121">**IaaS only**.</span></span> <span data-ttu-id="ed4f9-122">Solo puede habilitar VIP múltiples en servicios en la nube que contengan máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="ed4f9-123">No puede usar VIP múltiples en escenarios de PaaS, con instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="ed4f9-124">**Solo PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-124">**PowerShell only**.</span></span> <span data-ttu-id="ed4f9-125">Los VIP múltiples solo se pueden administrar mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="ed4f9-126">Estas limitaciones son temporales y pueden cambiar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="ed4f9-127">Asegúrese de volver a visitar esta página para comprobar los cambios futuros.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="ed4f9-128">Agregar una dirección VIP a un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="ed4f9-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="ed4f9-129">Para agregar una dirección VIP a su servicio, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="ed4f9-130">Este comando muestra un resultado similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="ed4f9-131">Eliminación de una dirección VIP de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="ed4f9-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="ed4f9-132">Para quitar la dirección VIP agregada al servicio en el  ejemplo anterior, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="ed4f9-133">Solo puede quitar una dirección VIP si no tiene ningún extremo asociado a ella.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="ed4f9-134">Recuperación de la información de dirección VIP de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="ed4f9-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="ed4f9-135">Para recuperar las direcciones VIP asociadas a un servicio en la nube, ejecute el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="ed4f9-136">El script muestra un resultado similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-136">The script displays a result similar to the following sample:</span></span>

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

<span data-ttu-id="ed4f9-137">En este ejemplo, el servicio en la nube tiene 3 direcciones VIP:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="ed4f9-138">**Vip1** es la dirección VIP predeterminada. Se sabe porque el valor de IsDnsProgrammedName está establecido en true.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="ed4f9-139">**Vip2** y **Vip3** no se usan, ya que no tienen ninguna dirección IP.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="ed4f9-140">Solo se usarán si asocia un extremo a la dirección VIP.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="ed4f9-141">Solo se cobrarán las direcciones VIP adicionales de su suscripción una vez que estén asociadas a un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="ed4f9-142">Para obtener más información sobre los precios, consulte [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="ed4f9-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="ed4f9-143">Asociación de una dirección VIP a un extremo</span><span class="sxs-lookup"><span data-stu-id="ed4f9-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="ed4f9-144">Para asociar una dirección VIP de un servicio en la nube a un extremo, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="ed4f9-145">El comando anterior crea un punto de conexión vinculado a la dirección VIP denominada *Vip2* en el puerto *80*, y lo vincula a la máquina virtual denominada *myVM1* en un servicio en la nube denominado *myService* con *TCP* en el puerto *8080*.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="ed4f9-146">Para comprobar la configuración, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="ed4f9-147">La salida es similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-147">The output looks similar to the following example:</span></span>

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

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="ed4f9-148">Habilitación del equilibrio de carga en una dirección VIP específica</span><span class="sxs-lookup"><span data-stu-id="ed4f9-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="ed4f9-149">Puede asociar una sola dirección VIP a varias máquinas virtuales con el fin de equilibrar la carga.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="ed4f9-150">Por ejemplo, suponga que tiene un servicio en la nube denominado *myService* y dos máquinas virtuales denominadas *myVM1* y *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="ed4f9-151">Y el servicio en la nube tiene varias direcciones VIP, una de ellas denominada *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="ed4f9-152">Si desea asegurarse de que todo el tráfico al puerto *81* en *Vip2* se equilibre entre *myVM1* y *myVM2* en el puerto *8181*, ejecute el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="ed4f9-153">También puede actualizar el equilibrador de carga para que use una dirección VIP diferente.</span><span class="sxs-lookup"><span data-stu-id="ed4f9-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="ed4f9-154">Por ejemplo, si ejecuta el siguiente comando de PowerShell, cambiará el conjunto de equilibrio de carga para que use una dirección VIP denominada Vip1:</span><span class="sxs-lookup"><span data-stu-id="ed4f9-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="ed4f9-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed4f9-155">Next Steps</span></span>

[<span data-ttu-id="ed4f9-156">Log Analytics para Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="ed4f9-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="ed4f9-157">Información general sobre el equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="ed4f9-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="ed4f9-158">Introducción al equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="ed4f9-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="ed4f9-159">Información general sobre redes virtuales</span><span class="sxs-lookup"><span data-stu-id="ed4f9-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="ed4f9-160">API de REST de IP reservada</span><span class="sxs-lookup"><span data-stu-id="ed4f9-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
