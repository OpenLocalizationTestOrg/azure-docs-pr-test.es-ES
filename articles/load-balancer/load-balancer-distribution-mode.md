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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="096b0-103">Configurar el modo de distribución de hello para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="096b0-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="096b0-104">Distribución basada en hash</span><span class="sxs-lookup"><span data-stu-id="096b0-104">Hash-based distribution mode</span></span>

<span data-ttu-id="096b0-105">algoritmo de distribución de Hello predeterminado es una tupla de 5 (del origen de IP, puerto de origen, dirección IP de destino, puerto de destino, el tipo de protocolo) servidores de toomap tráfico tooavailable de hash.</span><span class="sxs-lookup"><span data-stu-id="096b0-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="096b0-106">Dicho algoritmo solo proporciona adherencia dentro de una sesión de transporte.</span><span class="sxs-lookup"><span data-stu-id="096b0-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="096b0-107">Los paquetes de saludo será la misma sesión dirigen toohello instancia del mismo centro de datos IP (DIP) detrás de extremo con equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="096b0-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="096b0-108">Cuando se inicia el cliente de hello una nueva sesión de Hola misma IP de origen, puerto de origen de hello cambia y hace Hola tráfico toogo tooa DIP puntos de conexión diferentes.</span><span class="sxs-lookup"><span data-stu-id="096b0-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![equilibrador de carga basado en hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="096b0-110">Figura 1 - Distribución de 5-tupla</span><span class="sxs-lookup"><span data-stu-id="096b0-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="096b0-111">Modo de afinidad de IP de origen</span><span class="sxs-lookup"><span data-stu-id="096b0-111">Source IP affinity mode</span></span>

<span data-ttu-id="096b0-112">Tenemos un nuevo modo de distribución llamado Afinidad de IP de origen (también conocido como afinidad de cliente o afinidad de IP de cliente).</span><span class="sxs-lookup"><span data-stu-id="096b0-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="096b0-113">Equilibrador de carga de Azure puede ser toouse configurado una tupla de 2 (dirección IP de origen, dirección IP de destino) o toomap de tupla de 3 (protocolo IP de origen, dirección IP de destino,) el tráfico toohello de servidores disponibles.</span><span class="sxs-lookup"><span data-stu-id="096b0-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="096b0-114">Mediante el uso de afinidad de IP de origen, las conexiones inician desde Hola mismo equipo cliente deja de toohello mismo punto de conexión DIP.</span><span class="sxs-lookup"><span data-stu-id="096b0-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="096b0-115">Hola siguiente diagrama ilustra una configuración de la tupla de 2.</span><span class="sxs-lookup"><span data-stu-id="096b0-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="096b0-116">Tenga en cuenta cómo se ejecuta Hola tupla de 2 a través de hello carga equilibrador toovirtual máquina 1 (VM1) que es, a continuación, realizar copias de seguridad VM2 y VM3.</span><span class="sxs-lookup"><span data-stu-id="096b0-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![afinidad de la sesión](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="096b0-118">Figura 2 - Distribución de 2-tupla</span><span class="sxs-lookup"><span data-stu-id="096b0-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="096b0-119">Afinidad IP de origen resuelve una incompatibilidad entre Hola equilibrador de carga de Azure y puerta de enlace de escritorio remoto (RD).</span><span class="sxs-lookup"><span data-stu-id="096b0-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="096b0-120">Ahora, puede crear una granja de servidores de puerta de enlace de Escritorio remoto en un solo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="096b0-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="096b0-121">Otro escenario de caso de uso es la carga de medios donde la carga de datos de Hola se efectúa a través de UDP pero plano de control de Hola se logra a través de TCP:</span><span class="sxs-lookup"><span data-stu-id="096b0-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="096b0-122">Un cliente inicia una sesión TCP dirección pública de equilibrio de carga de toohello en primer lugar, obtiene tooa dirigido DIP específica, este canal está en estado de conexión de hello toomonitor active izquierdo</span><span class="sxs-lookup"><span data-stu-id="096b0-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="096b0-123">Una nueva sesión UDP de hello es el mismo equipo cliente inicia toohello extremo público con equilibrio de carga mismo, la expectativa de hello aquí es que esta conexión también está dirigido toohello mismo extremo DIP como conexión de TCP de hello anterior para que media carga puede ser se ejecuta en un alto rendimiento al tiempo que mantiene un canal de control a través de TCP.</span><span class="sxs-lookup"><span data-stu-id="096b0-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="096b0-124">Cuando cambia de un conjunto de carga equilibrada (quitar o agregar una máquina virtual), se vuelve a calcular la distribución de Hola de solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="096b0-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="096b0-125">No puede depender de las nuevas conexiones de los clientes existentes que terminan en hello mismo servidor.</span><span class="sxs-lookup"><span data-stu-id="096b0-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="096b0-126">Además, el uso del modo de distribución de afinidad de IP de origen puede ocasionar una distribución desigual del tráfico.</span><span class="sxs-lookup"><span data-stu-id="096b0-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="096b0-127">Los clientes que se ejecutan detrás de servidores proxy pueden considerarse como una sola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="096b0-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="096b0-128">Configuración de la afinidad de IP de origen para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="096b0-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="096b0-129">Para máquinas virtuales, puede utilizar opciones de tiempo de espera de toochange de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="096b0-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="096b0-130">Agregar una máquina Virtual tooa de extremo de Azure y establecer el modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="096b0-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="096b0-131">Se puede establecer LoadBalancerDistribution toosourceIP de tupla de 2 (dirección IP de origen, dirección IP de destino) de equilibrio de carga, sourceIPProtocol para equilibrio de carga de tupla de 3 (protocolo IP de origen, dirección IP de destino,) o ninguno si desea que el comportamiento predeterminado de Hola de equilibrio de carga de tupla de 5.</span><span class="sxs-lookup"><span data-stu-id="096b0-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="096b0-132">Usar hello después tooretrieve una configuración de modo de distribución del equilibrador de carga de punto de conexión:</span><span class="sxs-lookup"><span data-stu-id="096b0-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="096b0-133">Si hello LoadBalancerDistribution elemento no está presente equilibrador de carga de Azure de hello usa algoritmo de tupla de 5 Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="096b0-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="096b0-134">Establecer el modo de distribución de hello en un conjunto de extremos con equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="096b0-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="096b0-135">Si los puntos de conexión forman parte de un conjunto de extremos con equilibrio de carga, modo de distribución de hello debe establecerse en el conjunto de extremos con equilibrio de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="096b0-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="096b0-136">Modo de distribución de toochange de configuración de servicio de nube</span><span class="sxs-lookup"><span data-stu-id="096b0-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="096b0-137">Puede aprovechar hello Azure SDK para .NET 2.5 (toobe publicado en noviembre) tooupdate su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="096b0-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="096b0-138">Configuración de punto de conexión de servicios en la nube se realiza en .csdef Hola.</span><span class="sxs-lookup"><span data-stu-id="096b0-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="096b0-139">En orden tooupdate Hola carga equilibrador modo de distribución para una implementación de servicios en la nube, se requiere una actualización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="096b0-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="096b0-140">Este es un ejemplo de los cambios de .csdef para la configuración de extremo:</span><span class="sxs-lookup"><span data-stu-id="096b0-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="096b0-141">Ejemplo de API</span><span class="sxs-lookup"><span data-stu-id="096b0-141">API example</span></span>

<span data-ttu-id="096b0-142">Puede configurar la distribución de equilibrador de carga de hello mediante la API de administración de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="096b0-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="096b0-143">Realizar seguro hello tooadd `x-ms-version` encabezado se establece tooversion `2014-09-01` o superior.</span><span class="sxs-lookup"><span data-stu-id="096b0-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="096b0-144">Actualizar el conjunto de configuración de hello especificado con equilibrio de carga de hello en una implementación</span><span class="sxs-lookup"><span data-stu-id="096b0-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="096b0-145">Ejemplo de solicitud</span><span class="sxs-lookup"><span data-stu-id="096b0-145">Request example</span></span>

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

<span data-ttu-id="096b0-146">valor de Hola de LoadBalancerDistribution puede ser sourceIP para afinidad de tupla de 2, sourceIPProtocol para la afinidad de la tupla de 3 o ninguno (para sin afinidad.</span><span class="sxs-lookup"><span data-stu-id="096b0-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="096b0-147">es decir, 5-tupla).</span><span class="sxs-lookup"><span data-stu-id="096b0-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="096b0-148">Response</span><span class="sxs-lookup"><span data-stu-id="096b0-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="096b0-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="096b0-149">Next Steps</span></span>

[<span data-ttu-id="096b0-150">Información general sobre el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="096b0-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="096b0-151">Introducción a la configuración de un equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="096b0-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="096b0-152">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="096b0-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
