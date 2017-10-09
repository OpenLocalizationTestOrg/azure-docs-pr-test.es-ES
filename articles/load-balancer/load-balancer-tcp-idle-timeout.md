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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="71dd7-103">Modificación de la configuración de tiempo de espera de inactividad de TCP para Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="71dd7-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="71dd7-104">En su configuración predeterminada, Azure Load Balancer tiene una configuración de tiempo de espera de inactividad de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="71dd7-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="71dd7-105">Si un período de inactividad es mayor que el valor de tiempo de espera de hello, no hay ninguna garantía de que Hola TCP o se mantiene la sesión HTTP entre el cliente de Hola y el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="71dd7-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="71dd7-106">Cuando se cierra la conexión de hello, la aplicación cliente puede recibir Hola mensaje de error siguiente: "se cerró la conexión subyacente de hello: una conexión que se esperaba toobe mantiene activo se cerró por servidor hello."</span><span class="sxs-lookup"><span data-stu-id="71dd7-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="71dd7-107">Una práctica común es toouse un TCP keep-alive.</span><span class="sxs-lookup"><span data-stu-id="71dd7-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="71dd7-108">Esta práctica mantiene la conexión de hello activo durante un periodo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="71dd7-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="71dd7-109">Para obtener más información, consulte estos [ejemplos de .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="71dd7-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="71dd7-110">Con keep-alive habilitada, los paquetes se envían durante los períodos de inactividad en conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="71dd7-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="71dd7-111">Estos paquetes keep-alive Asegúrese de que nunca se alcanza el valor de tiempo de espera inactivo de Hola y Hola conexión se mantiene durante un largo período.</span><span class="sxs-lookup"><span data-stu-id="71dd7-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="71dd7-112">Esta configuración funciona solo para conexiones entrantes.</span><span class="sxs-lookup"><span data-stu-id="71dd7-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="71dd7-113">tooavoid al perder la conexión de hello, debe configurar Hola TCP persistente con un intervalo inferior Hola tiempo de espera inactivo configuración o aumente Hola tiempo de espera inactivo valor.</span><span class="sxs-lookup"><span data-stu-id="71dd7-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="71dd7-114">toosupport tales escenarios, hemos agregado compatibilidad para un tiempo de espera de inactividad configurable.</span><span class="sxs-lookup"><span data-stu-id="71dd7-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="71dd7-115">Ahora puede establecer para una duración de 4 minutos too30.</span><span class="sxs-lookup"><span data-stu-id="71dd7-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="71dd7-116">TCP Keep-alive funciona bien en escenarios donde la batería no supone una restricción.</span><span class="sxs-lookup"><span data-stu-id="71dd7-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="71dd7-117">No se recomienda para aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="71dd7-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="71dd7-118">Mediante un TCP keep-alive en una aplicación móvil puede agotar la batería del dispositivo de hello con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="71dd7-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![Tiempo de espera TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="71dd7-120">Hola las secciones siguientes describe cómo toochange inactivo de la configuración de tiempo de espera en las máquinas virtuales y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="71dd7-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="71dd7-121">Configurar el tiempo de espera de hello TCP para los minutos de too15 IP públicos de nivel de instancia</span><span class="sxs-lookup"><span data-stu-id="71dd7-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="71dd7-122">`IdleTimeoutInMinutes` es opcional.</span><span class="sxs-lookup"><span data-stu-id="71dd7-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="71dd7-123">Si no se establece, el tiempo de espera de hello predeterminado es 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="71dd7-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="71dd7-124">intervalo de tiempo de espera aceptable de Hello es 4 minutos too30.</span><span class="sxs-lookup"><span data-stu-id="71dd7-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="71dd7-125">Establecer tiempo de espera de inactividad de hello cuando se crea un extremo de Azure en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="71dd7-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="71dd7-126">toochange Hola tiempo de espera para un punto de conexión, utilice Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="71dd7-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="71dd7-127">tooretrieve la configuración del tiempo de espera inactivo, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="71dd7-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="71dd7-128">Establecer tiempo de espera TCP de hello en un conjunto de extremos con equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="71dd7-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="71dd7-129">Si los puntos de conexión forman parte de un conjunto de extremos con equilibrio de carga, el tiempo de espera de hello TCP debe establecerse en el conjunto de extremos con equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="71dd7-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="71dd7-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="71dd7-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="71dd7-131">Cambio de la configuración de tiempo de espera de los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="71dd7-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="71dd7-132">Puede usar hello Azure SDK tooupdate su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="71dd7-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="71dd7-133">Realizar una configuración de punto de conexión para servicios en la nube en el archivo de .csdef Hola.</span><span class="sxs-lookup"><span data-stu-id="71dd7-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="71dd7-134">Actualización del tiempo de espera TCP de hello para la implementación de un servicio de nube, requiere una actualización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="71dd7-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="71dd7-135">Una excepción es si se especifica el tiempo de espera de hello TCP solo para una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="71dd7-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="71dd7-136">Configuración de IP pública que se encuentran en el archivo de .cscfg de Hola y se puede actualizar a través de la actualización y actualización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="71dd7-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="71dd7-137">Hola .csdef cambios para la configuración de punto de conexión son:</span><span class="sxs-lookup"><span data-stu-id="71dd7-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="71dd7-138">Hola .cscfg cambios de configuración de tiempo de espera de hello en direcciones IP públicas son:</span><span class="sxs-lookup"><span data-stu-id="71dd7-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="71dd7-139">Ejemplo de API de REST</span><span class="sxs-lookup"><span data-stu-id="71dd7-139">REST API example</span></span>

<span data-ttu-id="71dd7-140">Puede configurar el tiempo de espera de inactividad de TCP Hola mediante API de administración de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="71dd7-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="71dd7-141">Asegúrese de que ese hello `x-ms-version` encabezado se establece tooversion `2014-06-01` o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="71dd7-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="71dd7-142">Actualizar la configuración del programa Hola Hola especifica extremos de entrada con equilibrio de carga en todas las máquinas virtuales en una implementación.</span><span class="sxs-lookup"><span data-stu-id="71dd7-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="71dd7-143">Solicitud</span><span class="sxs-lookup"><span data-stu-id="71dd7-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="71dd7-144">Response</span><span class="sxs-lookup"><span data-stu-id="71dd7-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="71dd7-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71dd7-145">Next steps</span></span>

[<span data-ttu-id="71dd7-146">Información general sobre el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="71dd7-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="71dd7-147">Introducción a la creación de un equilibrador de carga orientado a Internet</span><span class="sxs-lookup"><span data-stu-id="71dd7-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="71dd7-148">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="71dd7-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
