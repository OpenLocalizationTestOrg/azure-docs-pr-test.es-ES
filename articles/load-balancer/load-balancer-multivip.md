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
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Configuración de varias direcciones VIP para un servicio en la nube

Puede tener acceso a los servicios de nube de Azure a través de hello Internet pública mediante una dirección IP proporcionada por Azure. Esta dirección IP pública es tooas que se hace referencia una VIP (IP virtual) desde que se vinculó toohello Azure equilibrador de carga y no Hola instancias de máquina Virtual (VM) Hola del servicio en nube. Con una sola dirección VIP puede tener acceso a cualquier instancia de máquina virtual dentro de un servicio en la nube.

Sin embargo, hay escenarios en los que puede que necesite más de una VIP como un toohello de punto de entrada mismo servicio en la nube. Por ejemplo, el servicio de nube puede hospedar varios sitios Web que requieren conectividad SSL utiliza Hola puerto predeterminado 443, tal y como se hospeda cada sitio para un cliente diferente, o de inquilino. En este escenario, debe toohave una dirección IP pública con orientación diferente para cada sitio Web. Hello diagrama siguiente ilustra un hospedaje web multiempresa típica con una necesidad SSL varios certificados en hello mismo puerto público.

![Escenario SSL de varias direcciones VIP](./media/load-balancer-multivip/Figure1.png)

En el ejemplo de Hola anterior, todas las direcciones VIP uso Hola mismo puerto público (443) y el tráfico se tooone redirigida o más carga equilibrada de máquinas virtuales en un único puerto privado para la dirección IP interna de Hola de todos los sitios Web de Hola de hospedaje de servicio de nube de Hola.

> [!NOTE]
> Otra situación que requiera Hola uso Hola varias VIP hospeda varios agentes de escucha de grupo de disponibilidad de AlwaysOn de SQL en el mismo conjunto de máquinas virtuales de Hola.

VIP son dinámicas de forma predeterminada, lo que significa que puede cambiar Hola real dirección IP asignada toohello servicio en la nube con el tiempo. tooprevent que suceda, puede reservar a una VIP para el servicio. toolearn más información acerca de la VIP reservada, consulte [IP pública reservada](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Consulte [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obtener información sobre los precios de las direcciones VIP y las direcciones IP reservadas.

Puede usar PowerShell tooverify hello VIP utilizada los servicios de nube, así como agregar y quitar a VIP, asociar un punto de conexión de tooan VIP y configurar Equilibrio de carga en una sola dirección VIP específica.

## <a name="limitations"></a>Limitaciones

En este momento, la funcionalidad de varias VIP está limitado toohello los escenarios siguientes:

* **Solo IaaS**. Solo puede habilitar VIP múltiples en servicios en la nube que contengan máquinas virtuales. No puede usar VIP múltiples en escenarios de PaaS, con instancias de rol.
* **Solo PowerShell**. Los VIP múltiples solo se pueden administrar mediante PowerShell.

Estas limitaciones son temporales y pueden cambiar en cualquier momento. Asegúrese de toorevisit seguro de esta página tooverify los cambios futuros.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>¿Cómo tooadd una VIP tooa servicio en la nube
servicio de tooyour tooadd una VIP, ejecute el siguiente comando de PowerShell de hello:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Este comando muestra un toohello similar resultado según muestra:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>¿Cómo tooremove una VIP de un servicio de nube
Hola tooremove VIP agregados servicio tooyour en el ejemplo de Hola anteriormente, Hola ejecución siguiente comando de PowerShell:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> Sólo se puede quitar a una VIP si no tiene ningún tooit extremos asociados.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>La información de tooretrieve VIP de un servicio de nube
Hola tooretrieve VIP asociada a un servicio en la nube, ejecute el siguiente script de PowerShell de hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

script de Hola muestra un toohello similar resultado según muestra:

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

En este ejemplo, el servicio de nube de hello tiene 3 VIP:

* **Vip1** se Hola predeterminado VIP, sabrá que porque se establece el valor de Hola para IsDnsProgrammedName tootrue.
* **Vip2** y **Vip3** no se usan, ya que no tienen ninguna dirección IP. Sólo se utilizarán si asocia un toohello extremo VIP.

> [!NOTE]
> Solo se cobrarán las direcciones VIP adicionales de su suscripción una vez que estén asociadas a un punto de conexión. Para obtener más información sobre los precios, consulte [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>¿Cómo tooassociate una VIP tooan extremo

tooassociate una VIP en un extremo de tooan de servicio de nube, ejecute el siguiente comando de PowerShell de hello:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

comando Hello crea un extremo VIP toohello vinculado llamado *Vip2* en el puerto *80*y se proporcionan vínculos toohello máquina virtual denominada *myVM1* en un servicio de nube denominado * myService* con *TCP* en el puerto *8080*.

configuración de hello tooverify, ejecute el siguiente comando de PowerShell de hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

salida de Hello tiene un aspecto similar toohello siguiente ejemplo:

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>¿Cómo tooenable equilibrio de carga en una sola dirección VIP específica

Puede asociar una sola dirección VIP a varias máquinas virtuales con el fin de equilibrar la carga. Por ejemplo, suponga que tiene un servicio en la nube denominado *myService* y dos máquinas virtuales denominadas *myVM1* y *myVM2*. Y el servicio en la nube tiene varias direcciones VIP, una de ellas denominada *Vip2*. Si desea que todo el tráfico tooport de tooensure *81* en *Vip2* se equilibra entre *myVM1* y *myVM2* en el puerto *8181 *, ejecute hello siguiente script de PowerShell:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

También puede actualizar su toouse de equilibrador de carga una VIP diferente. Por ejemplo, si ejecuta Hola comando de PowerShell a continuación, cambiará el conjunto toouse una VIP con el nombre de la Vip1 de equilibrio de carga de hello:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Pasos siguientes

[Log Analytics para Azure Load Balancer](load-balancer-monitor-log.md)

[Información general sobre el equilibrador de carga accesible desde Internet](load-balancer-internet-overview.md)

[Introducción al equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md)

[Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md)

[API de REST de IP reservada](https://msdn.microsoft.com/library/azure/dn722420.aspx)
