---
title: "Configuración del tiempo de espera de inactividad de TCP de Load Balancer | Microsoft Docs"
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
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="a6afc-103">Modificación de la configuración de tiempo de espera de inactividad de TCP para Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="a6afc-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="a6afc-104">En su configuración predeterminada, Azure Load Balancer tiene una configuración de tiempo de espera de inactividad de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="a6afc-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="a6afc-105">Si un período de inactividad es mayor que el valor de tiempo de espera, no hay ninguna garantía de que todavía exista la sesión TCP o HTTP entre el cliente y el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="a6afc-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="a6afc-106">Cuando se cierra la conexión, la aplicación cliente recibirá un mensaje de error similar a "Se ha terminado la conexión subyacente: una conexión que se esperaba que se mantuviera activa fue cerrada por el servidor".</span><span class="sxs-lookup"><span data-stu-id="a6afc-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="a6afc-107">Una práctica común es usar TCP Keep-alive.</span><span class="sxs-lookup"><span data-stu-id="a6afc-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="a6afc-108">Esta práctica mantiene la conexión activa durante un periodo más largo.</span><span class="sxs-lookup"><span data-stu-id="a6afc-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="a6afc-109">Para obtener más información, consulte estos [ejemplos de .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6afc-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="a6afc-110">Con Keep-alive habilitado, los paquetes se envían durante los periodos de inactividad en la conexión.</span><span class="sxs-lookup"><span data-stu-id="a6afc-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="a6afc-111">Estos paquetes de Keep-alive garantizan que nunca se alcance el valor de tiempo de espera de inactividad y la conexión se mantenga durante un largo período.</span><span class="sxs-lookup"><span data-stu-id="a6afc-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="a6afc-112">Esta configuración funciona solo para conexiones entrantes.</span><span class="sxs-lookup"><span data-stu-id="a6afc-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="a6afc-113">Para evitar la pérdida de la conexión, debe configurar TCP keep-alive con un intervalo menor que el valor de tiempo de espera de inactividad o aumentar el valor de tiempo de espera de inactividad.</span><span class="sxs-lookup"><span data-stu-id="a6afc-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="a6afc-114">Para admitir tales escenarios, hemos agregado compatibilidad con un tiempo de espera de inactividad configurable.</span><span class="sxs-lookup"><span data-stu-id="a6afc-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="a6afc-115">Ahora puede establecer una duración de entre 4 y 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="a6afc-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="a6afc-116">TCP Keep-alive funciona bien en escenarios donde la batería no supone una restricción.</span><span class="sxs-lookup"><span data-stu-id="a6afc-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="a6afc-117">No se recomienda para aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="a6afc-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="a6afc-118">El uso de TCP Keep-alive desde una aplicación móvil puede agotarla batería del dispositivo más rápidamente.</span><span class="sxs-lookup"><span data-stu-id="a6afc-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![Tiempo de espera TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="a6afc-120">Las secciones siguientes describen cómo cambiar la configuración de tiempo de espera de inactividad en máquinas virtuales y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="a6afc-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="a6afc-121">Configuración del tiempo de espera de TCP para la IP pública a nivel de instancia en 15 minutos</span><span class="sxs-lookup"><span data-stu-id="a6afc-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="a6afc-122">`IdleTimeoutInMinutes` es opcional.</span><span class="sxs-lookup"><span data-stu-id="a6afc-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="a6afc-123">Si no se establece, el tiempo de espera predeterminado es de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="a6afc-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="a6afc-124">El intervalo de tiempo de espera aceptable está entre 4 y 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="a6afc-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="a6afc-125">Establecimiento del tiempo de espera de inactividad al crear un punto de conexión de Azure en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a6afc-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="a6afc-126">Para cambiar la configuración de tiempo de espera de un punto de conexión, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a6afc-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="a6afc-127">Para recuperar la configuración de tiempo de espera de inactividad, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a6afc-127">To retrieve your idle timeout configuration, use the following command:</span></span>

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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="a6afc-128">Establecimiento del tiempo de espera de TCP en un conjunto de puntos de conexión de carga equilibrada</span><span class="sxs-lookup"><span data-stu-id="a6afc-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="a6afc-129">Si los puntos de conexión forman parte de un conjunto de extremo de carga equilibrada, el tiempo de espera de TCP se debe establecer en el conjunto de punto de conexión de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="a6afc-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="a6afc-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a6afc-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="a6afc-131">Cambio de la configuración de tiempo de espera de los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="a6afc-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="a6afc-132">Puede aprovechar Azure SDK para actualizar el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="a6afc-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="a6afc-133">La configuración de punto de conexión para los servicios en la nube se realiza en el archivo .csdef.</span><span class="sxs-lookup"><span data-stu-id="a6afc-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="a6afc-134">La actualización del tiempo de espera de TCP para la implementación de un servicio en la nube requiere una actualización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="a6afc-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="a6afc-135">Se da una excepción si el tiempo de espera de TCP solo se especifica para una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="a6afc-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="a6afc-136">La configuración de IP pública se encuentra en el archivo .cscfg y se puede actualizar a través de la actualización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="a6afc-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="a6afc-137">Los cambios de .csdef para la configuración de extremo son:</span><span class="sxs-lookup"><span data-stu-id="a6afc-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="a6afc-138">Los cambios de .cscfg para el valor de tiempo de espera en las direcciones IP públicas son:</span><span class="sxs-lookup"><span data-stu-id="a6afc-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="a6afc-139">Ejemplo de API de REST</span><span class="sxs-lookup"><span data-stu-id="a6afc-139">REST API example</span></span>

<span data-ttu-id="a6afc-140">Puede configurar el tiempo de espera de inactividad de TCP mediante Service Management API.</span><span class="sxs-lookup"><span data-stu-id="a6afc-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="a6afc-141">Asegúrese de que el encabezado `x-ms-version` esté establecido en la versión `2014-06-01` o posterior.</span><span class="sxs-lookup"><span data-stu-id="a6afc-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="a6afc-142">Actualice la configuración de los puntos de conexión de entrada de carga equilibrada especificados en todas las máquinas virtuales de una implementación.</span><span class="sxs-lookup"><span data-stu-id="a6afc-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="a6afc-143">Solicitud</span><span class="sxs-lookup"><span data-stu-id="a6afc-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="a6afc-144">Response</span><span class="sxs-lookup"><span data-stu-id="a6afc-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a6afc-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6afc-145">Next steps</span></span>

[<span data-ttu-id="a6afc-146">Información general sobre el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="a6afc-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="a6afc-147">Introducción a la creación de un equilibrador de carga orientado a Internet</span><span class="sxs-lookup"><span data-stu-id="a6afc-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="a6afc-148">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a6afc-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
