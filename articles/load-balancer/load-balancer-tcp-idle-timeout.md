---
title: tiempo de espera de inactividad de TCP de equilibrador de carga aaaConfigure | Documentos de Microsoft
description: "Configuración del tiempo de espera de inactividad de TCP de Load Balancer"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Modificación de la configuración de tiempo de espera de inactividad de TCP para Azure Load Balancer

En su configuración predeterminada, Azure Load Balancer tiene una configuración de tiempo de espera de inactividad de 4 minutos. Si un período de inactividad es mayor que el valor de tiempo de espera de hello, no hay ninguna garantía de que Hola TCP o se mantiene la sesión HTTP entre el cliente de Hola y el servicio en la nube.

Cuando se cierra la conexión de hello, la aplicación cliente puede recibir Hola mensaje de error siguiente: "se cerró la conexión subyacente de hello: una conexión que se esperaba toobe mantiene activo se cerró por servidor hello."

Una práctica común es toouse un TCP keep-alive. Esta práctica mantiene la conexión de hello activo durante un periodo de tiempo. Para obtener más información, consulte estos [ejemplos de .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Con keep-alive habilitada, los paquetes se envían durante los períodos de inactividad en conexiones de Hola. Estos paquetes keep-alive Asegúrese de que nunca se alcanza el valor de tiempo de espera inactivo de Hola y Hola conexión se mantiene durante un largo período.

Esta configuración funciona solo para conexiones entrantes. tooavoid al perder la conexión de hello, debe configurar Hola TCP persistente con un intervalo inferior Hola tiempo de espera inactivo configuración o aumente Hola tiempo de espera inactivo valor. toosupport tales escenarios, hemos agregado compatibilidad para un tiempo de espera de inactividad configurable. Ahora puede establecer para una duración de 4 minutos too30.

TCP Keep-alive funciona bien en escenarios donde la batería no supone una restricción. No se recomienda para aplicaciones móviles. Mediante un TCP keep-alive en una aplicación móvil puede agotar la batería del dispositivo de hello con mayor rapidez.

![Tiempo de espera TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

Hola las secciones siguientes describe cómo toochange inactivo de la configuración de tiempo de espera en las máquinas virtuales y servicios en la nube.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Configurar el tiempo de espera de hello TCP para los minutos de too15 IP públicos de nivel de instancia

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` es opcional. Si no se establece, el tiempo de espera de hello predeterminado es 4 minutos. intervalo de tiempo de espera aceptable de Hello es 4 minutos too30.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Establecer tiempo de espera de inactividad de hello cuando se crea un extremo de Azure en una máquina virtual

toochange Hola tiempo de espera para un punto de conexión, utilice Hola siguiente:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve la configuración del tiempo de espera inactivo, Hola de uso siguiente comando:

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Establecer tiempo de espera TCP de hello en un conjunto de extremos con equilibrio de carga

Si los puntos de conexión forman parte de un conjunto de extremos con equilibrio de carga, el tiempo de espera de hello TCP debe establecerse en el conjunto de extremos con equilibrio de carga de Hola. Por ejemplo:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Cambio de la configuración de tiempo de espera de los servicios en la nube

Puede usar hello Azure SDK tooupdate su servicio en la nube. Realizar una configuración de punto de conexión para servicios en la nube en el archivo de .csdef Hola. Actualización del tiempo de espera TCP de hello para la implementación de un servicio de nube, requiere una actualización de la implementación. Una excepción es si se especifica el tiempo de espera de hello TCP solo para una dirección IP pública. Configuración de IP pública que se encuentran en el archivo de .cscfg de Hola y se puede actualizar a través de la actualización y actualización de la implementación.

Hola .csdef cambios para la configuración de punto de conexión son:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

Hola .cscfg cambios de configuración de tiempo de espera de hello en direcciones IP públicas son:

```xml
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
    <InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
        <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
    </InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="rest-api-example"></a>Ejemplo de API de REST

Puede configurar el tiempo de espera de inactividad de TCP Hola mediante API de administración de servicios de Hola. Asegúrese de que ese hello `x-ms-version` encabezado se establece tooversion `2014-06-01` o una versión posterior. Actualizar la configuración del programa Hola Hola especifica extremos de entrada con equilibrio de carga en todas las máquinas virtuales en una implementación.

### <a name="request"></a>Solicitud

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Response

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a>Pasos siguientes

[Información general sobre el equilibrador de carga interno](load-balancer-internal-overview.md)

[Introducción a la creación de un equilibrador de carga orientado a Internet](load-balancer-get-started-internet-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)
