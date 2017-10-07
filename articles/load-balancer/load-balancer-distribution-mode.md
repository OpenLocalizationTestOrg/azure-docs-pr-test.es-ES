---
title: "modo de distribución del equilibrador de carga de aaaConfigure | Documentos de Microsoft"
description: "Cómo tooconfigure Azure afinidad de IP de origen de toosupport modo de distribución de equilibrador de carga"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Configurar el modo de distribución de hello para el equilibrador de carga

## <a name="hash-based-distribution-mode"></a>Distribución basada en hash

algoritmo de distribución de Hello predeterminado es una tupla de 5 (del origen de IP, puerto de origen, dirección IP de destino, puerto de destino, el tipo de protocolo) servidores de toomap tráfico tooavailable de hash. Dicho algoritmo solo proporciona adherencia dentro de una sesión de transporte. Los paquetes de saludo será la misma sesión dirigen toohello instancia del mismo centro de datos IP (DIP) detrás de extremo con equilibrio de carga de Hola. Cuando se inicia el cliente de hello una nueva sesión de Hola misma IP de origen, puerto de origen de hello cambia y hace Hola tráfico toogo tooa DIP puntos de conexión diferentes.

![equilibrador de carga basado en hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Figura 1 - Distribución de 5-tupla

## <a name="source-ip-affinity-mode"></a>Modo de afinidad de IP de origen

Tenemos un nuevo modo de distribución llamado Afinidad de IP de origen (también conocido como afinidad de cliente o afinidad de IP de cliente). Equilibrador de carga de Azure puede ser toouse configurado una tupla de 2 (dirección IP de origen, dirección IP de destino) o toomap de tupla de 3 (protocolo IP de origen, dirección IP de destino,) el tráfico toohello de servidores disponibles. Mediante el uso de afinidad de IP de origen, las conexiones inician desde Hola mismo equipo cliente deja de toohello mismo punto de conexión DIP.

Hola siguiente diagrama ilustra una configuración de la tupla de 2. Tenga en cuenta cómo se ejecuta Hola tupla de 2 a través de hello carga equilibrador toovirtual máquina 1 (VM1) que es, a continuación, realizar copias de seguridad VM2 y VM3.

![afinidad de la sesión](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Figura 2 - Distribución de 2-tupla

Afinidad IP de origen resuelve una incompatibilidad entre Hola equilibrador de carga de Azure y puerta de enlace de escritorio remoto (RD). Ahora, puede crear una granja de servidores de puerta de enlace de Escritorio remoto en un solo servicio en la nube.

Otro escenario de caso de uso es la carga de medios donde la carga de datos de Hola se efectúa a través de UDP pero plano de control de Hola se logra a través de TCP:

* Un cliente inicia una sesión TCP dirección pública de equilibrio de carga de toohello en primer lugar, obtiene tooa dirigido DIP específica, este canal está en estado de conexión de hello toomonitor active izquierdo
* Una nueva sesión UDP de hello es el mismo equipo cliente inicia toohello extremo público con equilibrio de carga mismo, la expectativa de hello aquí es que esta conexión también está dirigido toohello mismo extremo DIP como conexión de TCP de hello anterior para que media carga puede ser se ejecuta en un alto rendimiento al tiempo que mantiene un canal de control a través de TCP.

> [!NOTE]
> Cuando cambia de un conjunto de carga equilibrada (quitar o agregar una máquina virtual), se vuelve a calcular la distribución de Hola de solicitudes de cliente. No puede depender de las nuevas conexiones de los clientes existentes que terminan en hello mismo servidor. Además, el uso del modo de distribución de afinidad de IP de origen puede ocasionar una distribución desigual del tráfico. Los clientes que se ejecutan detrás de servidores proxy pueden considerarse como una sola aplicación cliente.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Configuración de la afinidad de IP de origen para el equilibrador de carga

Para máquinas virtuales, puede utilizar opciones de tiempo de espera de toochange de PowerShell:

Agregar una máquina Virtual tooa de extremo de Azure y establecer el modo de distribución del equilibrador de carga

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

Se puede establecer LoadBalancerDistribution toosourceIP de tupla de 2 (dirección IP de origen, dirección IP de destino) de equilibrio de carga, sourceIPProtocol para equilibrio de carga de tupla de 3 (protocolo IP de origen, dirección IP de destino,) o ninguno si desea que el comportamiento predeterminado de Hola de equilibrio de carga de tupla de 5.

Usar hello después tooretrieve una configuración de modo de distribución del equilibrador de carga de punto de conexión:

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

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
    LoadBalancerDistribution : sourceIP

Si hello LoadBalancerDistribution elemento no está presente equilibrador de carga de Azure de hello usa algoritmo de tupla de 5 Hola predeterminado.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Establecer el modo de distribución de hello en un conjunto de extremos con equilibrio de carga

Si los puntos de conexión forman parte de un conjunto de extremos con equilibrio de carga, modo de distribución de hello debe establecerse en el conjunto de extremos con equilibrio de carga de hello:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Modo de distribución de toochange de configuración de servicio de nube

Puede aprovechar hello Azure SDK para .NET 2.5 (toobe publicado en noviembre) tooupdate su servicio en la nube. Configuración de punto de conexión de servicios en la nube se realiza en .csdef Hola. En orden tooupdate Hola carga equilibrador modo de distribución para una implementación de servicios en la nube, se requiere una actualización de la implementación.
Este es un ejemplo de los cambios de .csdef para la configuración de extremo:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
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

## <a name="api-example"></a>Ejemplo de API

Puede configurar la distribución de equilibrador de carga de hello mediante la API de administración de servicios de Hola. Realizar seguro hello tooadd `x-ms-version` encabezado se establece tooversion `2014-09-01` o superior.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Actualizar el conjunto de configuración de hello especificado con equilibrio de carga de hello en una implementación

#### <a name="request-example"></a>Ejemplo de solicitud

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

valor de Hola de LoadBalancerDistribution puede ser sourceIP para afinidad de tupla de 2, sourceIPProtocol para la afinidad de la tupla de 3 o ninguno (para sin afinidad. es decir, 5-tupla).

#### <a name="response"></a>Response

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Pasos siguientes

[Información general sobre el equilibrador de carga interno](load-balancer-internal-overview.md)

[Introducción a la configuración de un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
