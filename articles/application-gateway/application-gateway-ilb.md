---
title: Uso de Azure Application Gateway con el equilibrador de carga interno | Microsoft Docs
description: "Esta página proporciona instrucciones para configurar una puerta de enlace de aplicaciones de Azure con un extremo de equilibrio de carga interno"
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
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="ea079-103">Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)</span><span class="sxs-lookup"><span data-stu-id="ea079-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea079-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea079-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="ea079-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ea079-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="ea079-106">La Puerta de enlace de aplicaciones se puede configurar con una IP virtual accesible desde Internet o con un punto de conexión interno no expuesto a Internet, lo que se conoce también como punto de conexión de Equilibrador de carga interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="ea079-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="ea079-107">Configurar la puerta de enlace con un ILB es útil para las aplicaciones de línea de negocio internas que no se exponen en Internet.</span><span class="sxs-lookup"><span data-stu-id="ea079-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="ea079-108">También es útil para los servicios o niveles dentro de una aplicación de varios niveles que se asientan en un límite de seguridad no expuesto a Internet, pero que siguen necesitando distribución de carga round robin, permanencia de sesión o terminación SSL.</span><span class="sxs-lookup"><span data-stu-id="ea079-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="ea079-109">Este artículo le guía por los pasos necesarios para configurar una puerta de enlace de aplicaciones con un ILB.</span><span class="sxs-lookup"><span data-stu-id="ea079-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ea079-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ea079-110">Before you begin</span></span>

1. <span data-ttu-id="ea079-111">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="ea079-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="ea079-112">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la [Página de descarga](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ea079-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="ea079-113">Compruebe que tiene una red virtual que funciona con una subred válida.</span><span class="sxs-lookup"><span data-stu-id="ea079-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="ea079-114">Compruebe que dispone de servidores backend, ya sea en la red virtual o con una dirección IP virtual o dirección IP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="ea079-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="ea079-115">Para crear una puerta de enlace de aplicaciones, realice los pasos siguientes en el orden mostrado.</span><span class="sxs-lookup"><span data-stu-id="ea079-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="ea079-116">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea079-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="ea079-117">Configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="ea079-118">Establecimiento de la configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="ea079-119">Inicio de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="ea079-120">Comprobación de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="ea079-121">Creación de una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="ea079-121">Create an application gateway:</span></span>

<span data-ttu-id="ea079-122">**Para crear la puerta de enlace**, use el cmdlet `New-AzureApplicationGateway` y reemplace los valores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="ea079-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="ea079-123">Tenga en cuenta que la facturación de la puerta de enlace no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="ea079-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="ea079-124">La facturación comienza en un paso posterior, cuando la puerta de enlace se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ea079-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

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

<span data-ttu-id="ea079-125">**Para validar** la creación de la puerta de enlace, puede usar el cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="ea079-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="ea079-126">En el ejemplo, *Description*, *InstanceCount* y *GatewaySize* son parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="ea079-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="ea079-127">El valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="ea079-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="ea079-128">El valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="ea079-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="ea079-129">Small y Large son otros valores disponibles.</span><span class="sxs-lookup"><span data-stu-id="ea079-129">Small and Large are other available values.</span></span> <span data-ttu-id="ea079-130">*Vip* y *DnsName* se muestran en blanco porque todavía no se ha iniciado la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="ea079-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="ea079-131">Se crearán una vez que la puerta de enlace esté en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ea079-131">These are created once the gateway is in the running state.</span></span> 

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

## <a name="configure-the-gateway"></a><span data-ttu-id="ea079-132">Configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-132">Configure the gateway</span></span>
<span data-ttu-id="ea079-133">Una configuración de puerta de enlace de aplicaciones consta de varios valores.</span><span class="sxs-lookup"><span data-stu-id="ea079-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="ea079-134">Los valores pueden ir juntos para construir la configuración.</span><span class="sxs-lookup"><span data-stu-id="ea079-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="ea079-135">Los valores son:</span><span class="sxs-lookup"><span data-stu-id="ea079-135">The values are:</span></span>

* <span data-ttu-id="ea079-136">**Grupo de servidores de backend:** lista de direcciones IP de los servidores backend.</span><span class="sxs-lookup"><span data-stu-id="ea079-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="ea079-137">Las direcciones IP mostradas deben pertenecer a la subred de red virtual o deben ser una dirección IP virtual o dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="ea079-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="ea079-138">**Configuración del grupo de servidores back-end** : cada grupo tiene una configuración como el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="ea079-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="ea079-139">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="ea079-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="ea079-140">**Puerto front-end:** este puerto es el puerto público abierto en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ea079-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="ea079-141">El tráfico llega a este puerto y, a continuación, se redirige a uno de los servidores backend.</span><span class="sxs-lookup"><span data-stu-id="ea079-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="ea079-142">**Agente de escucha** : la escucha tiene un puerto front-end, un protocolo (Http o Https, estos distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="ea079-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="ea079-143">**Regla:** enlaza el agente de escucha y el grupo de servidores backend, y define a qué grupo de servidores backend se debe dirigir el tráfico cuando llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="ea079-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="ea079-144">Actualmente, solo se admite la regla *básica* .</span><span class="sxs-lookup"><span data-stu-id="ea079-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="ea079-145">La regla *basic* regla es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="ea079-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="ea079-146">Puede llevar a cabo la configuración mediante la creación de un objeto de configuración o usando un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="ea079-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="ea079-147">Para llevar a cabo la configuración usando un archivo XML de configuración, use el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ea079-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="ea079-148">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ea079-148">Note the following:</span></span>

* <span data-ttu-id="ea079-149">El elemento *FrontendIPConfigurations* describe los detalles del ILB relevantes para configurar la Puerta de enlace de aplicaciones con un ILB.</span><span class="sxs-lookup"><span data-stu-id="ea079-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="ea079-150">El elemento *Type* de la dirección IP del front-end debe establecerse en 'Private'</span><span class="sxs-lookup"><span data-stu-id="ea079-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="ea079-151">El elemento *StaticIPAddress* debe establecerse en la dirección IP interna deseada en el que la puerta de enlace recibe el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ea079-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="ea079-152">Tenga en cuenta que el elemento *StaticIPAddress* es opcional.</span><span class="sxs-lookup"><span data-stu-id="ea079-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="ea079-153">Si no se establece, se elige una dirección IP interna disponible de la subred implementada.</span><span class="sxs-lookup"><span data-stu-id="ea079-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="ea079-154">El valor del elemento *Name* especificado en *FrontendIPConfiguration* se debe usar en el elemento *FrontendIP* de HTTPListener para hacer referencia a FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="ea079-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="ea079-155">**Ejemplo XML de configuración**</span><span class="sxs-lookup"><span data-stu-id="ea079-155">**Configuration XML sample**</span></span>
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


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="ea079-156">Establecimiento de la configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-156">Set the gateway configuration</span></span>
<span data-ttu-id="ea079-157">A continuación, establecerá la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ea079-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="ea079-158">Puede usar el cmdlet `Set-AzureApplicationGatewayConfig` con un objeto de configuración o con un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="ea079-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-the-gateway"></a><span data-ttu-id="ea079-159">Inicio de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-159">Start the gateway</span></span>

<span data-ttu-id="ea079-160">Una vez configurada la puerta de enlace, use el cmdlet `Start-AzureApplicationGateway` para iniciarla.</span><span class="sxs-lookup"><span data-stu-id="ea079-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="ea079-161">La facturación de una puerta de enlace de aplicaciones comienza después de que se haya iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ea079-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="ea079-162">La regla `Start-AzureApplicationGateway` puede tardar hasta 15-20 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="ea079-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
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

## <a name="verify-the-gateway-status"></a><span data-ttu-id="ea079-163">Comprobación del estado de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ea079-163">Verify the gateway status</span></span>

<span data-ttu-id="ea079-164">Use el cmdlet `Get-AzureApplicationGateway` para comprobar el estado de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="ea079-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="ea079-165">Si el cmdlet `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior, el valor de State debería ser *Running* (En ejecución) y Vip y DnsName deben tener entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="ea079-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="ea079-166">Este ejemplo muestra el cmdlet en la primera línea, seguido de la salida.</span><span class="sxs-lookup"><span data-stu-id="ea079-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="ea079-167">En este ejemplo, la puerta de enlace se está ejecutando y está lista para asumir tráfico.</span><span class="sxs-lookup"><span data-stu-id="ea079-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="ea079-168">La puerta de enlace de aplicaciones está configurada para aceptar tráfico en el punto de conexión del ILB configurado: 10.0.0.10 en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ea079-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ea079-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea079-169">Next steps</span></span>
<span data-ttu-id="ea079-170">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="ea079-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="ea079-171">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="ea079-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="ea079-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ea079-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

