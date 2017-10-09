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
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>Primeros pasos en la creación de un equilibrador de carga interno (clásico) mediante PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloud Services](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Crear un equilibrador de carga interno establecido para máquinas virtuales

toocreate un equilibrador de carga interno establecido y Hola servidores que enviarán su tráfico tooit, tiene el mensaje de error toodo Hola siguientes:

1. Cree una instancia de interno equilibrio de carga que será el punto de conexión de Hola de carga de toobe tráfico entrante están equilibrada en los servidores de Hola de un conjunto con equilibrio de carga.
2. Agregue extremos correspondientes máquinas virtuales de toohello que va a recibir el tráfico entrante Hola.
3. Configure los servidores de Hola que van a enviar equilibrio de carga de hello tráfico toobe toosend su tráfico toohello dirección IP virtual (VIP) de instancia de equilibrio de carga interno de Hola.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>Paso 1: crear una instancia de Equilibrio de carga interno

Para un servicio de nube existente o un servicio de nube implementado en una red virtual regional, puede crear una instancia de equilibrio de carga interno con hello después de comandos de Windows PowerShell:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Tenga en cuenta que este uso de hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) cmdlet de Windows PowerShell usa Hola de parámetros defaultprobe. Para obtener más información sobre conjuntos de parámetros adicionales, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>Paso 2: Agregar instancia del equilibrio de carga interno de toohello de puntos de conexión

Aquí tiene un ejemplo:

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

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>Paso 3: Configurar su toosend servidores su extremo de equilibrio de carga interno nuevo de tráfico toohello

Demasiado ha configurar servidores de hello cuyo tráfico es continuo toobe con equilibrio de carga toouse Hola nueva dirección IP (Hola VIP) del programa Hola a instancia de equilibrio de carga interno. Se trata de una dirección de hello en qué Hola equilibrio de carga interno está escuchando la instancia. En la mayoría de los casos, deberá toojust agregar o modificar un registro DNS para hello VIP de instancia de equilibrio de carga interno de Hola.

Si especifica la dirección IP de Hola durante la creación de hello de instancia de equilibrio de carga interno de hello, ya tiene Hola VIP. En caso contrario, puede ver a Hola VIP de hello siguientes comandos:

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse estos comandos, rellene los valores de hello y quitar Hola < y >. Aquí tiene un ejemplo:

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

En pantalla de Hola de hello comando Get-AzureInternalLoadBalancer, anote la dirección IP de Hola y que servidores de tooyour de cambios necesarios de Hola o tooensure de registros DNS que el tráfico se envía a toohello VIP estén.

> [!NOTE]
> plataforma de Microsoft Azure de Hello usa una dirección IPv4 estática, enrutable públicamente para una amplia variedad de escenarios de administración. dirección IP de Hello es 168.63.129.16. Ningún firewall debe bloquear esta dirección IP, ya que puede causar un comportamiento inesperado.
> Con sentido tooAzure de equilibrio de carga interno, se usa esta dirección IP mediante la supervisión de sondeos de estado de mantenimiento de Hola de toodetermine equilibrador de carga de Hola para máquinas virtuales en un conjunto de carga equilibrada. Si un grupo de seguridad de red es toorestrict usado tráfico tooAzure máquinas en un conjunto de carga equilibrada internamente o aplicado tooa subred de red Virtual, asegúrese de que una regla de seguridad de red se agrega tráfico tooallow desde 168.63.129.16.

## <a name="example-of-internal-load-balancing"></a>Ejemplo de equilibrio de carga interno

toostep le guía por hello final tooend proceso de creación de un conjunto de carga equilibrada para dos configuraciones de ejemplo, vea Hola siguientes secciones.

### <a name="an-internet-facing-multi-tier-application"></a>Una aplicación de niveles múltiples accesible desde Internet

Desea tooprovide un servicio de base de datos con equilibrio de carga para un conjunto de servidores web de conexión a Internet. Ambos conjuntos de servidores se hospedan en un solo servicio en la nube de Azure. Puerto 1433 de la tooTCP de tráfico del servidor Web debe distribuirse entre las dos máquinas virtuales en el nivel de base de datos de Hola. La figura 1 muestra la configuración de Hola.

![Conjunto de equilibrio de carga interno para el nivel de base de datos de Hola](./media/load-balancer-internal-getstarted/IC736321.png)

configuración de Hello consta de los siguientes hello:

* servicio de Hello existente en la nube que hospeda máquinas virtuales de Hola se denomina mytestcloud.
* dos servidores de base de datos existente Hola se denominan DB1, DB2.
* Servidores Web en el nivel de web Hola conectan toohello servidores de base de datos en el nivel de base de datos de hello mediante el uso de direcciones IP privadas de Hola. Otra opción es toouse su propio DNS para la red virtual de Hola y registrar manualmente un registro a para el conjunto de equilibrador de carga interno de Hola.

Hello comandos siguientes configuran una nueva instancia de equilibrio de carga interno denominada **ILBset** y agregar máquinas virtuales extremos toohello que correspondiente toohello dos servidores de base de datos:

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

## <a name="remove-an-internal-load-balancing-configuration"></a>Quitar una configuración de Equilibrio de carga interno

tooremove una máquina virtual como un punto de conexión de una instancia de equilibrador de carga interno, Hola de uso después de comandos:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse estos comandos, rellene los valores de hello, quitar Hola < y >.

Aquí tiene un ejemplo:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove una instancia de equilibrador de carga interno de un servicio de nube, Hola de uso siguientes comandos:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

toouse estos comandos, complete el valor de Hola y quite Hola < y >.

Aquí tiene un ejemplo:

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>Información adicional sobre los cmdlet de equilibrador de carga interno

tooobtain información adicional acerca de los cmdlets de equilibrio de carga interno, ejecute hello siga los comandos en un símbolo del sistema de Windows PowerShell:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Pasos siguientes

[Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)

