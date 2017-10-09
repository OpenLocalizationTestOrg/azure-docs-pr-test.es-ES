---
title: puerta de enlace de aplicaciones de Azure con el equilibrador de carga interno aaaUsing | Documentos de Microsoft
description: "Esta página proporcionan instrucciones tooconfigure una puerta de enlace de aplicaciones de Azure con un extremo con equilibrio de carga interno"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="05c69-103">Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)</span><span class="sxs-lookup"><span data-stu-id="05c69-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="05c69-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="05c69-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="05c69-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="05c69-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="05c69-106">Puerta de enlace de aplicaciones puede configurarse con un orientado a dirección IP virtual de internet o con un extremo interno no expuesta toohello internet, también conocido como punto de conexión de equilibrador de carga interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="05c69-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="05c69-107">Configurar puerta de enlace de hello con un ILB es útil para aplicaciones de línea de negocio internas no expuestas toointernet.</span><span class="sxs-lookup"><span data-stu-id="05c69-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="05c69-108">También es útil para los niveles de servicio/dentro de una aplicación de varios niveles, que se encuentra en un toointernet no expuesto el límite de seguridad, pero aún requieren la distribución de la carga de round robin, adherencia de sesión o terminación SSL.</span><span class="sxs-lookup"><span data-stu-id="05c69-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="05c69-109">Este artículo le guiará a través de hello pasos tooconfigure una puerta de enlace de la aplicación con un ILB.</span><span class="sxs-lookup"><span data-stu-id="05c69-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="05c69-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="05c69-110">Before you begin</span></span>

1. <span data-ttu-id="05c69-111">Instale la versión más reciente de los cmdlets de PowerShell de Azure de hello usan Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="05c69-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="05c69-112">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descarga](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="05c69-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="05c69-113">Compruebe que tiene una red virtual que funciona con una subred válida.</span><span class="sxs-lookup"><span data-stu-id="05c69-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="05c69-114">Compruebe que dispone de servidores back-end en la red virtual de hello, o con una dirección IP pública/VIP asignada.</span><span class="sxs-lookup"><span data-stu-id="05c69-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="05c69-115">toocreate una puerta de enlace de aplicaciones, realizar Hola pasos en orden de hello indicado.</span><span class="sxs-lookup"><span data-stu-id="05c69-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="05c69-116">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="05c69-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="05c69-117">Configurar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="05c69-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="05c69-118">Configuración de puerta de enlace de Hola de conjunto</span><span class="sxs-lookup"><span data-stu-id="05c69-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="05c69-119">Iniciar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="05c69-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="05c69-120">Compruebe la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="05c69-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="05c69-121">Creación de una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="05c69-121">Create an application gateway:</span></span>

<span data-ttu-id="05c69-122">**puerta de enlace de hello toocreate**, usar hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="05c69-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="05c69-123">Tenga en cuenta que la facturación de puerta de enlace de hello no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="05c69-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="05c69-124">Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="05c69-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="05c69-125">**toovalidate** que se creó la puerta de enlace de hello, puede usar hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05c69-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="05c69-126">En el ejemplo de Hola, *descripción*, *InstanceCount*, y *GatewaySize* son parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="05c69-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="05c69-127">Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="05c69-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="05c69-128">Hola valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="05c69-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="05c69-129">Small y Large son otros valores disponibles.</span><span class="sxs-lookup"><span data-stu-id="05c69-129">Small and Large are other available values.</span></span> <span data-ttu-id="05c69-130">*VIP* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="05c69-131">Estos se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-131">These are created once hello gateway is in hello running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a><span data-ttu-id="05c69-132">Configurar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="05c69-132">Configure hello gateway</span></span>
<span data-ttu-id="05c69-133">Una configuración de puerta de enlace de aplicaciones consta de varios valores.</span><span class="sxs-lookup"><span data-stu-id="05c69-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="05c69-134">se pueden acumular los valores de Hello configuración de hello tooconstruct juntos.</span><span class="sxs-lookup"><span data-stu-id="05c69-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="05c69-135">los valores de Hello son:</span><span class="sxs-lookup"><span data-stu-id="05c69-135">hello values are:</span></span>

* <span data-ttu-id="05c69-136">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="05c69-137">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="05c69-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="05c69-138">**Configuración del grupo de servidores back-end** : cada grupo tiene una configuración como el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="05c69-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="05c69-139">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="05c69-140">**Puerto de front-end:** este puerto es el puerto público Hola abierto en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="05c69-141">Tráfico llega a este puerto y, a continuación, obtiene redirigida tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="05c69-142">**Agente de escucha:** agente de escucha de hello tiene un puerto de front-end, un protocolo (Http o Https, estos distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="05c69-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="05c69-143">**Regla:** regla Hola enlaza el agente de escucha de Hola y de grupo de servidores de back-end de Hola y define qué tráfico de hello del grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="05c69-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="05c69-144">Actualmente, solo Hola *básico* se admite la regla.</span><span class="sxs-lookup"><span data-stu-id="05c69-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="05c69-145">Hola *básica* regla es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="05c69-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="05c69-146">Puede llevar a cabo la configuración mediante la creación de un objeto de configuración o usando un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="05c69-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="05c69-147">tooconstruct la configuración mediante el uso de un archivo XML de configuración, use Hola de ejemplo a continuación.</span><span class="sxs-lookup"><span data-stu-id="05c69-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="05c69-148">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="05c69-148">Note hello following:</span></span>

* <span data-ttu-id="05c69-149">Hola *FrontendIPConfigurations* elemento describe hello ILB detalles pertinentes para configurar la puerta de enlace de aplicaciones con un ILB.</span><span class="sxs-lookup"><span data-stu-id="05c69-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="05c69-150">IP de front-end Hello *tipo* debe establecerse too'Private'</span><span class="sxs-lookup"><span data-stu-id="05c69-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="05c69-151">Hola *StaticIPAddress* debe establecerse en qué Hola puerta de enlace recibe el tráfico IP interna toohello deseado.</span><span class="sxs-lookup"><span data-stu-id="05c69-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="05c69-152">Tenga en cuenta que hello *StaticIPAddress* elemento es opcional.</span><span class="sxs-lookup"><span data-stu-id="05c69-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="05c69-153">Si no es así conjunto, se elige una IP interna disponible de la subred de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="05c69-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="05c69-154">Hola valo hello *nombre* especificado en el elemento *FrontendIPConfiguration* debe usarse en hello HTTPListener *FrontendIP* toohello toorefer de elemento FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="05c69-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="05c69-155">**Ejemplo XML de configuración**</span><span class="sxs-lookup"><span data-stu-id="05c69-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="05c69-156">Configuración de puerta de enlace de Hola de conjunto</span><span class="sxs-lookup"><span data-stu-id="05c69-156">Set hello gateway configuration</span></span>
<span data-ttu-id="05c69-157">A continuación, se establecerá la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="05c69-158">Puede usar hello `Set-AzureApplicationGatewayConfig` cmdlet con un objeto de configuración, o con un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="05c69-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a><span data-ttu-id="05c69-159">Iniciar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="05c69-159">Start hello gateway</span></span>

<span data-ttu-id="05c69-160">Una vez que se ha configurado la puerta de enlace de hello, usar hello `Start-AzureApplicationGateway` puerta de enlace de cmdlet toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="05c69-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="05c69-161">La facturación de una puerta de enlace de la aplicación comienza después de puerta de enlace de Hola se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="05c69-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="05c69-162">Hola `Start-AzureApplicationGateway` cmdlet podría tardar hasta toocomplete too15-20 minutos.</span><span class="sxs-lookup"><span data-stu-id="05c69-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="05c69-163">Comprobar el estado de la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="05c69-163">Verify hello gateway status</span></span>

<span data-ttu-id="05c69-164">Hola de uso `Get-AzureApplicationGateway` estado de cmdlet toocheck Hola de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="05c69-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="05c69-165">Si `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior de hello, estado de hello debería ser *ejecuta*, Hola Vip y DnsName debe tener las entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="05c69-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="05c69-166">Ejemplo hello cmdlet muestra en la primera línea hello, seguido de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="05c69-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="05c69-167">En este ejemplo, puerta de enlace de hello está ejecutando y está listo tootake tráfico.</span><span class="sxs-lookup"><span data-stu-id="05c69-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="05c69-168">se configura la puerta de enlace de aplicaciones de Hello tooaccept tráfico en hello configurado extremo ILB de 10.0.0.10 en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="05c69-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="05c69-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05c69-169">Next steps</span></span>
<span data-ttu-id="05c69-170">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="05c69-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="05c69-171">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="05c69-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="05c69-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="05c69-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

