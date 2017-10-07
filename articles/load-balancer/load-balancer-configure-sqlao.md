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
# <a name="configure-load-balancer-for-sql-always-on"></a>Configuración del equilibrador de carga para SQL Always On

Los grupos de disponibilidad de SQL Server AlwaysOn se pueden ejecutar ahora con ILB. El grupo de disponibilidad es la solución estrella de SQL Server para conseguir alta disponibilidad y recuperación ante desastres. Hola agente de escucha del grupo de disponibilidad permite a las aplicaciones cliente tooseamlessly conectar la réplica principal de toohello, independientemente del número de Hola de réplicas de hello en la configuración de Hola.

nombre de (dominio DNS) del agente de escucha de Hello es la dirección IP de tooa asignada con equilibrio de carga y equilibrador de carga de Azure indica el servidor principal de Hola entrantes tráfico tooonly Hola Hola conjunto de réplica.

Puede usar ILB para los extremos de SQL Server AlwaysOn (escucha). Ahora tiene control sobre la accesibilidad de Hola de agente de escucha de Hola y elegir dirección IP con equilibrio de carga de Hola desde una subred específica de la red Virtual (VNet).

Mediante el uso de ILB en el agente de escucha de hello, Hola el punto de conexión SQL server (por ejemplo, Server = tcp:ListenerName, 1433; base de datos = DatabaseName) solo es accesible para:

* Servicios y máquinas virtuales en Hola misma red Virtual
* Servicios y máquinas virtuales de redes locales conectadas
* Servicios y máquinas virtuales de redes virtuales interconectadas

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Figura 1 - SQL AlwaysOn configurado con equilibrador de carga accesible desde Internet

## <a name="add-internal-load-balancer-toohello-service"></a>Agregar servicio de toohello de equilibrador de carga interno

1. En el siguiente ejemplo de Hola, configuramos una red Virtual que contiene una subred llamada "Subred-1":

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Agregue los extremos con equilibrio de carga para ILB en cada máquina virtual.

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    En el ejemplo de Hola anterior, tiene 2 VM llamado "sqlsvc1" y "sqlsvc2" ejecutar "Sqlsvc" del servicio en nube de Hola. Después de crear Hola ILB con `DirectServerReturn` cambiar, agregar extremos con equilibrio toohello ILB tooallow SQL tooconfigure Hola agentes de escucha para grupos de disponibilidad de Hola de carga.

Para más información sobre SQL AlwaysOn, consulte [Configuración de un equilibrador de carga interno para un grupo de disponibilidad AlwaysOn de Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Otras referencias
[Introducción a la configuración de un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md)

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
