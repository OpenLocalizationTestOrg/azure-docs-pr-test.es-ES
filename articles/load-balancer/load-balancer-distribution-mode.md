---
title: "Configuración de un modo de distribución de Load Balancer | Microsoft Docs"
description: "Cómo configurar el modo de distribución del equilibrador de carga de Azure para admitir la afinidad de IP de origen"
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
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="d376c-103">Configuración del modo de distribución en el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d376c-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="d376c-104">Distribución basada en hash</span><span class="sxs-lookup"><span data-stu-id="d376c-104">Hash-based distribution mode</span></span>

<span data-ttu-id="d376c-105">El algoritmo de distribución predeterminado para asignar el tráfico a los servidores disponibles es un hash de 5-tupla (IP de origen, puerto de origen, IP de destino, puerto de destino, tipo de protocolo).</span><span class="sxs-lookup"><span data-stu-id="d376c-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="d376c-106">Dicho algoritmo solo proporciona adherencia dentro de una sesión de transporte.</span><span class="sxs-lookup"><span data-stu-id="d376c-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="d376c-107">Los paquetes de la misma sesión se dirigirán a la misma instancia de IP del centro de datos (DIP) tras el punto de conexión con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="d376c-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="d376c-108">Cuando el cliente inicia una nueva sesión desde la misma IP de origen, el puerto de origen cambia y provoca que el tráfico vaya hacia otro punto de conexión DIP.</span><span class="sxs-lookup"><span data-stu-id="d376c-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![equilibrador de carga basado en hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="d376c-110">Figura 1 - Distribución de 5-tupla</span><span class="sxs-lookup"><span data-stu-id="d376c-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="d376c-111">Modo de afinidad de IP de origen</span><span class="sxs-lookup"><span data-stu-id="d376c-111">Source IP affinity mode</span></span>

<span data-ttu-id="d376c-112">Tenemos un nuevo modo de distribución llamado Afinidad de IP de origen (también conocido como afinidad de cliente o afinidad de IP de cliente).</span><span class="sxs-lookup"><span data-stu-id="d376c-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="d376c-113">Para asignar el tráfico a los servidores disponibles, se puede configurar Azure Load Balancer para usar una 2-tupla (IP de origen, IP de destino) o una 3-tupla (IP de origen, IP de destino, protocolo).</span><span class="sxs-lookup"><span data-stu-id="d376c-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="d376c-114">Al usar la afinidad de IP de origen, las conexiones iniciadas desde el mismo equipo cliente van al mismo extremo DIP.</span><span class="sxs-lookup"><span data-stu-id="d376c-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="d376c-115">En el siguiente diagrama, se ilustra una configuración de 2-tupla.</span><span class="sxs-lookup"><span data-stu-id="d376c-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="d376c-116">Observe cómo la 2-tupla se ejecuta a través del equilibrador de carga en la máquina virtual 1 (VM1) de la que luego VM2 y VM3 realizan una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d376c-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![afinidad de la sesión](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="d376c-118">Figura 2 - Distribución de 2-tupla</span><span class="sxs-lookup"><span data-stu-id="d376c-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="d376c-119">La afinidad de IP de origen resuelve una incompatibilidad entre Azure Load Balancer y la Puerta de enlace de Escritorio remoto (RD).</span><span class="sxs-lookup"><span data-stu-id="d376c-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="d376c-120">Ahora, puede crear una granja de servidores de puerta de enlace de Escritorio remoto en un solo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="d376c-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="d376c-121">Otro caso de uso es la carga de contenido multimedia donde la carga de los datos tiene lugar a través de UDP pero el plano de control se consigue mediante TCP:</span><span class="sxs-lookup"><span data-stu-id="d376c-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="d376c-122">Un cliente inicia primero una sesión TCP en la dirección pública con equilibrio de carga y se le dirige a una DIP específica; este canal se deja activo para supervisar el estado de conexión.</span><span class="sxs-lookup"><span data-stu-id="d376c-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="d376c-123">Una nueva sesión UDP se inicia desde el mismo equipo cliente en el mismo extremo público con equilibrio de carga. Lo que se espera aquí, es que esta conexión también se dirija al mismo extremo DIP que la conexión TCP anterior, de modo que la carga de contenido multimedia se pueda ejecutar con un elevado rendimiento, al mismo tiempo que se mantiene también un canal de control a través de TCP.</span><span class="sxs-lookup"><span data-stu-id="d376c-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="d376c-124">Cuando el conjunto con equilibrio de carga cambia (al quitar o agregar una máquina virtual), la distribución de las solicitudes de cliente se vuelve a calcular.</span><span class="sxs-lookup"><span data-stu-id="d376c-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="d376c-125">No puede depender de nuevas conexiones desde clientes existentes que terminan en el mismo servidor.</span><span class="sxs-lookup"><span data-stu-id="d376c-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="d376c-126">Además, el uso del modo de distribución de afinidad de IP de origen puede ocasionar una distribución desigual del tráfico.</span><span class="sxs-lookup"><span data-stu-id="d376c-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="d376c-127">Los clientes que se ejecutan detrás de servidores proxy pueden considerarse como una sola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="d376c-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="d376c-128">Configuración de la afinidad de IP de origen para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d376c-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="d376c-129">En las máquinas virtuales, puede usar PowerShell para cambiar la configuración de tiempo de espera:</span><span class="sxs-lookup"><span data-stu-id="d376c-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="d376c-130">Agregar un extremo de Azure a una máquina virtual y establecer el modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d376c-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="d376c-131">LoadBalancerDistribution puede establecerse en sourceIP para equilibrio de carga de 2-tupla (dirección IP de origen, dirección IP de destino), en sourceIPProtocol para equilibrio de carga de 3-tupla (dirección IP de origen, IP de destino, protocolo) o en ninguno si desea el comportamiento predeterminado de equilibrio de carga de 5-tupla.</span><span class="sxs-lookup"><span data-stu-id="d376c-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="d376c-132">Utilice lo siguiente para recuperar una configuración de modo de distribución del equilibrador de carga de punto de conexión:</span><span class="sxs-lookup"><span data-stu-id="d376c-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="d376c-133">Si el elemento LoadBalancerDistribution no está presente, el Equilibrador de carga de Azure usa el algoritmo predeterminado de 5-tupla.</span><span class="sxs-lookup"><span data-stu-id="d376c-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="d376c-134">Establecer el modo de distribución en un conjunto de extremo de carga equilibrada</span><span class="sxs-lookup"><span data-stu-id="d376c-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="d376c-135">Si los extremos forman parte de un conjunto de extremos con equilibrio de carga, el modo de distribución debe establecerse en el conjunto de extremos con equilibrio de carga:</span><span class="sxs-lookup"><span data-stu-id="d376c-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="d376c-136">Configuración de servicios en la nube para cambiar el modo de distribución</span><span class="sxs-lookup"><span data-stu-id="d376c-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="d376c-137">Puede aprovechar el SDK de Azure para .NET 2.5 (que se publicará en noviembre) para actualizar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="d376c-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="d376c-138">La configuración de extremo para los servicios en la nube se realiza en el archivo .csdef.</span><span class="sxs-lookup"><span data-stu-id="d376c-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="d376c-139">Para actualizar el modo de distribución del equilibrador de carga para una implementación de servicios en la nube, se requiere una actualización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="d376c-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="d376c-140">Este es un ejemplo de los cambios de .csdef para la configuración de extremo:</span><span class="sxs-lookup"><span data-stu-id="d376c-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="d376c-141">Ejemplo de API</span><span class="sxs-lookup"><span data-stu-id="d376c-141">API example</span></span>

<span data-ttu-id="d376c-142">Puede configurar la distribución del equilibrador de carga con Service Management API.</span><span class="sxs-lookup"><span data-stu-id="d376c-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="d376c-143">Asegúrese de agregar el encabezado `x-ms-version` y que esté establecido en la versión `2014-09-01` o posterior.</span><span class="sxs-lookup"><span data-stu-id="d376c-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="d376c-144">Actualizar la configuración del conjunto de carga equilibrada especificado en una implementación</span><span class="sxs-lookup"><span data-stu-id="d376c-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="d376c-145">Ejemplo de solicitud</span><span class="sxs-lookup"><span data-stu-id="d376c-145">Request example</span></span>

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

<span data-ttu-id="d376c-146">El valor de LoadBalancerDistribution puede ser sourceIP para la afinidad de 2-tupla, sourceIPProtocol para la afinidad de 3-tupla o ninguno (sin afinidad,</span><span class="sxs-lookup"><span data-stu-id="d376c-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="d376c-147">es decir, 5-tupla).</span><span class="sxs-lookup"><span data-stu-id="d376c-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="d376c-148">Response</span><span class="sxs-lookup"><span data-stu-id="d376c-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="d376c-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d376c-149">Next Steps</span></span>

[<span data-ttu-id="d376c-150">Información general sobre el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="d376c-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="d376c-151">Introducción a la configuración de un equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="d376c-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="d376c-152">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="d376c-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
