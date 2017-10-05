---
title: "Creación, inicio o eliminación de una puerta de enlace de aplicaciones | Microsoft Docs"
description: "Esta página proporciona instrucciones para crear, configurar, iniciar y eliminar una Puerta de enlace de aplicaciones de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: c4932096229b1941e0966e7f3e97de39c6931392
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="f00a7-103">Creación, inicio o eliminación de una puerta de enlace de aplicaciones con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f00a7-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f00a7-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f00a7-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="f00a7-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f00a7-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="f00a7-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="f00a7-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="f00a7-107">Plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f00a7-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="f00a7-108">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f00a7-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="f00a7-109">Puerta de enlace de aplicaciones de Azure es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="f00a7-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="f00a7-110">Proporciona conmutación por error, solicitudes HTTP de enrutamiento de rendimiento entre distintos servidores, independientemente de que se encuentren en la nube o en una implementación local.</span><span class="sxs-lookup"><span data-stu-id="f00a7-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="f00a7-111">Application Gateway proporciona numerosas características del Controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, etc.</span><span class="sxs-lookup"><span data-stu-id="f00a7-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="f00a7-112">Para obtener una lista completa de las características admitidas, visite [Introducción a Application Gateway](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="f00a7-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="f00a7-113">Este artículo le guiará por los pasos necesarios para crear, configurar, iniciar y eliminar una Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f00a7-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f00a7-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f00a7-114">Before you begin</span></span>

1. <span data-ttu-id="f00a7-115">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="f00a7-115">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="f00a7-116">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la [página Descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f00a7-116">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f00a7-117">Si tiene una red virtual existente, seleccione una subred vacía existente o cree una nueva subred en la red virtual existente, únicamente para uso de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f00a7-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="f00a7-118">No se puede implementar la puerta de enlace de la aplicación en una red virtual diferente de los recursos que se van a implementar detrás de la puerta de enlace de aplicaciones a menos que se utilice el emparejamiento de VNET.</span><span class="sxs-lookup"><span data-stu-id="f00a7-118">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway unless vnet peering is used.</span></span> <span data-ttu-id="f00a7-119">Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f00a7-119">To learn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="f00a7-120">Compruebe que tiene una red virtual de trabajo con una subred válida.</span><span class="sxs-lookup"><span data-stu-id="f00a7-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="f00a7-121">Asegúrese de que ninguna máquina virtual o implementación en la nube usan la subred.</span><span class="sxs-lookup"><span data-stu-id="f00a7-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="f00a7-122">La Puerta de enlace de aplicaciones debe encontrarse en una subred de red virtual.</span><span class="sxs-lookup"><span data-stu-id="f00a7-122">The application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="f00a7-123">Los servidores que configure para que usen la Puerta de enlace de aplicaciones deben existir, o bien sus puntos de conexión deben haberse creado en la red virtual o tener una dirección IP/VIP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="f00a7-123">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="f00a7-124">¿Qué se necesita para crear una Puerta de enlace de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="f00a7-124">What is required to create an application gateway?</span></span>

<span data-ttu-id="f00a7-125">Si se usa el comando `New-AzureApplicationGateway` para crear la puerta de enlace de aplicaciones, no se define ninguna configuración en ese momento y el recurso recién creado se configura con XML o con un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-125">When you use the `New-AzureApplicationGateway` command to create the application gateway, no configuration is set at this point and the newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="f00a7-126">Los valores son:</span><span class="sxs-lookup"><span data-stu-id="f00a7-126">The values are:</span></span>

* <span data-ttu-id="f00a7-127">**Grupo de servidores back-end** : lista de direcciones IP de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="f00a7-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="f00a7-128">Las direcciones IP que se enumeran deben pertenecer a la subred de la red virtual o ser una IP/VIP pública.</span><span class="sxs-lookup"><span data-stu-id="f00a7-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="f00a7-129">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="f00a7-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f00a7-130">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="f00a7-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="f00a7-131">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f00a7-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="f00a7-132">El tráfico llega a este puerto y después se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="f00a7-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="f00a7-133">**Agente de escucha** : tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="f00a7-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f00a7-134">**Regla** : enlaza el agente de escucha y el grupo de servidores back-end y define a qué grupo de servidores back-end se dirigirá el tráfico cuando llega a un agente de escucha concreto.</span><span class="sxs-lookup"><span data-stu-id="f00a7-134">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="f00a7-135">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f00a7-135">Create an application gateway</span></span>

<span data-ttu-id="f00a7-136">Para crear una Puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="f00a7-136">To create an application gateway:</span></span>

1. <span data-ttu-id="f00a7-137">Cree un recurso de Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f00a7-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="f00a7-138">Cree un archivo de configuración XML o un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="f00a7-139">Confirme la configuración para el recurso de la Puerta de enlace de aplicaciones recién creado.</span><span class="sxs-lookup"><span data-stu-id="f00a7-139">Commit the configuration to the newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="f00a7-140">Si necesita configurar un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [Creación de una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f00a7-140">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="f00a7-141">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="f00a7-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Escenario de ejemplo][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="f00a7-143">Crear un recurso de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f00a7-143">Create an application gateway resource</span></span>

<span data-ttu-id="f00a7-144">Para crear la puerta de enlace, use el cmdlet `New-AzureApplicationGateway` y reemplace los valores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="f00a7-144">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="f00a7-145">La facturación de la puerta de enlace no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="f00a7-145">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="f00a7-146">La facturación comienza en un paso posterior, cuando la puerta de enlace se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f00a7-146">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="f00a7-147">En el ejemplo siguiente se crea una puerta de enlace de aplicaciones mediante una red virtual denominada "testvnet1" y una subred llamada "subnet-1":</span><span class="sxs-lookup"><span data-stu-id="f00a7-147">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="f00a7-148">*Description*, *InstanceCount* y *GatewaySize* son parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="f00a7-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="f00a7-149">Para validar la creación de la puerta de enlace, puede usar el cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="f00a7-149">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="f00a7-150">El valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="f00a7-150">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="f00a7-151">El valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="f00a7-151">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="f00a7-152">Puede elegir entre Pequeño, Mediano y Grande.</span><span class="sxs-lookup"><span data-stu-id="f00a7-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="f00a7-153">*VirtualIPs* y *DnsName* se muestran en blanco porque todavía no se ha iniciado la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f00a7-153">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="f00a7-154">Se crearán una vez que la puerta de enlace esté en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f00a7-154">These are created once the gateway is in the running state.</span></span>

## <a name="configure-the-application-gateway"></a><span data-ttu-id="f00a7-155">Configuración de la Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f00a7-155">Configure the application gateway</span></span>

<span data-ttu-id="f00a7-156">La Puerta de enlace de aplicaciones se puede configurar con un archivo XML o con un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-156">You can configure the application gateway by using XML or a configuration object.</span></span>

### <a name="configure-the-application-gateway-by-using-xml"></a><span data-ttu-id="f00a7-157">Configuración de una Puerta de enlace de aplicaciones mediante XML</span><span class="sxs-lookup"><span data-stu-id="f00a7-157">Configure the application gateway by using XML</span></span>

<span data-ttu-id="f00a7-158">En el ejemplo siguiente, se usa un archivo XML para configurar todos los valores de la puerta de enlace de aplicaciones y confirmarlos en el recurso de dicha puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f00a7-158">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="f00a7-159">Paso 1</span><span class="sxs-lookup"><span data-stu-id="f00a7-159">Step 1</span></span>

<span data-ttu-id="f00a7-160">Copie el texto siguiente y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f00a7-160">Copy the following text to Notepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="f00a7-161">Edite los valores entre paréntesis de los elementos de configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-161">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="f00a7-162">Guarde el archivo con extensión .xml.</span><span class="sxs-lookup"><span data-stu-id="f00a7-162">Save the file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f00a7-163">El elemento de protocolo Http o Https distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f00a7-163">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="f00a7-164">En el ejemplo siguiente se muestra cómo usar un archivo de configuración para configurar Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f00a7-164">The following example shows how to use a configuration file to set up the application gateway.</span></span> <span data-ttu-id="f00a7-165">La carga de ejemplo equilibra el tráfico HTTP en el puerto público 80 y envía tráfico de red al puerto 80 de back-end entre dos direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="f00a7-165">The example load balances HTTP traffic on public port 80 and sends network traffic to back-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a><span data-ttu-id="f00a7-166">Paso 2</span><span class="sxs-lookup"><span data-stu-id="f00a7-166">Step 2</span></span>

<span data-ttu-id="f00a7-167">Después, establezca la Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f00a7-167">Next, set the application gateway.</span></span> <span data-ttu-id="f00a7-168">Use el cmdlet `Set-AzureApplicationGatewayConfig` con un archivo de configuración XML.</span><span class="sxs-lookup"><span data-stu-id="f00a7-168">Use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-the-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="f00a7-169">Configuración de la Puerta de enlace de aplicaciones con un objeto de configuración</span><span class="sxs-lookup"><span data-stu-id="f00a7-169">Configure the application gateway by using a configuration object</span></span>

<span data-ttu-id="f00a7-170">En el ejemplo siguiente, se muestra cómo configurar la Puerta de enlace de aplicaciones con objetos de configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-170">The following example shows how to configure the application gateway by using configuration objects.</span></span> <span data-ttu-id="f00a7-171">Todos los elementos de configuración deben configurarse individualmente y, a continuación, se deben agregar a un objeto de configuración de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f00a7-171">All configuration items must be configured individually and then added to an application gateway configuration object.</span></span> <span data-ttu-id="f00a7-172">Después de crear el objeto de configuración, use el comando `Set-AzureApplicationGateway` para confirmar la configuración del recurso de puerta de enlace de aplicaciones creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f00a7-172">After creating the configuration object, you use the `Set-AzureApplicationGateway` command to commit the configuration to the previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="f00a7-173">Antes de asignar un valor a cada objeto de configuración, es preciso declarar el tipo de objeto que usa PowerShell para el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f00a7-173">Before assigning a value to each configuration object, you need to declare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="f00a7-174">La primera línea para crear los elementos individuales define qué `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` se usan.</span><span class="sxs-lookup"><span data-stu-id="f00a7-174">The first line to create the individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="f00a7-175">Paso 1</span><span class="sxs-lookup"><span data-stu-id="f00a7-175">Step 1</span></span>

<span data-ttu-id="f00a7-176">Cree todos los elementos de configuración individuales.</span><span class="sxs-lookup"><span data-stu-id="f00a7-176">Create all individual configuration items.</span></span>

<span data-ttu-id="f00a7-177">Cree la IP de front-end, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="f00a7-177">Create the front-end IP as shown in the following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="f00a7-178">Cree el puerto front-end, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="f00a7-178">Create the front-end port as shown in the following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="f00a7-179">Cree el grupo de servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="f00a7-179">Create the back-end server pool.</span></span>

<span data-ttu-id="f00a7-180">Defina las direcciones IP que se agregan al grupo de servidores back-end como se muestra en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f00a7-180">Define the IP addresses that are added to the back-end server pool as shown in the next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="f00a7-181">Utilice el objeto $server para agregar los valores al objeto del grupo de servidores back-end ($pool)</span><span class="sxs-lookup"><span data-stu-id="f00a7-181">Use the $server object to add the values to the back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="f00a7-182">Cree la configuración del grupo de servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="f00a7-182">Create the back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="f00a7-183">Cree el agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="f00a7-183">Create the listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="f00a7-184">Cree la regla.</span><span class="sxs-lookup"><span data-stu-id="f00a7-184">Create the rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="f00a7-185">Paso 2</span><span class="sxs-lookup"><span data-stu-id="f00a7-185">Step 2</span></span>

<span data-ttu-id="f00a7-186">Asigne todos los elementos de configuración individuales a un objeto de configuración de la Puerta de enlace de aplicaciones ($appgwconfig):</span><span class="sxs-lookup"><span data-stu-id="f00a7-186">Assign all individual configuration items to an application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="f00a7-187">Agregue la IP front-end a la configuración</span><span class="sxs-lookup"><span data-stu-id="f00a7-187">Add the front-end IP to the configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="f00a7-188">Agregue el puerto front-end a la configuración</span><span class="sxs-lookup"><span data-stu-id="f00a7-188">Add the front-end port to the configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="f00a7-189">Agregue el grupo de servidores back-end a la configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-189">Add the back-end server pool to the configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="f00a7-190">Agregue la configuración del grupo back-end a la configuración</span><span class="sxs-lookup"><span data-stu-id="f00a7-190">Add the back-end pool setting to the configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="f00a7-191">Agregue el agente de escucha a la configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-191">Add the listener to the configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="f00a7-192">Agregue la regla a la configuración.</span><span class="sxs-lookup"><span data-stu-id="f00a7-192">Add the rule to the configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="f00a7-193">Paso 3</span><span class="sxs-lookup"><span data-stu-id="f00a7-193">Step 3</span></span>
<span data-ttu-id="f00a7-194">Confirme el objeto de configuración en el recurso de puerta de enlace de aplicaciones con `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="f00a7-194">Commit the configuration object to the application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-the-gateway"></a><span data-ttu-id="f00a7-195">Inicio de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="f00a7-195">Start the gateway</span></span>

<span data-ttu-id="f00a7-196">Una vez configurada la puerta de enlace, use el cmdlet `Start-AzureApplicationGateway` para iniciarla.</span><span class="sxs-lookup"><span data-stu-id="f00a7-196">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="f00a7-197">La facturación de una puerta de enlace de aplicaciones comienza después de que se haya iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="f00a7-197">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="f00a7-198">La regla `Start-AzureApplicationGateway` puede tardar hasta 15-20 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="f00a7-198">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="f00a7-199">Comprobación del estado de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="f00a7-199">Verify the gateway status</span></span>

<span data-ttu-id="f00a7-200">Use el cmdlet `Get-AzureApplicationGateway` para comprobar el estado de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f00a7-200">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="f00a7-201">Si el cmdlet `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior, el valor de *State* debería ser Running (En ejecución) y *Vip* y *DnsName* deben tener entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="f00a7-201">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="f00a7-202">En el siguiente ejemplo se muestra una puerta de enlace de aplicaciones activa y que está lista para recibir el tráfico destinado a `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="f00a7-202">The following example shows an application gateway that is up, running, and ready to take traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="f00a7-203">Eliminación de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f00a7-203">Delete the application gateway</span></span>

<span data-ttu-id="f00a7-204">Para eliminar la puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f00a7-204">To delete the application gateway:</span></span>

1. <span data-ttu-id="f00a7-205">Use el cmdlet `Stop-AzureApplicationGateway` para detener la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f00a7-205">Use the `Stop-AzureApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="f00a7-206">Utilice el cmdlet `Remove-AzureApplicationGateway` para quitar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f00a7-206">Use the `Remove-AzureApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="f00a7-207">Compruebe que se quitó la puerta de enlace con el cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="f00a7-207">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="f00a7-208">En el siguiente ejemplo se muestra el cmdlet `Stop-AzureApplicationGateway` en la primera línea, seguido de la salida.</span><span class="sxs-lookup"><span data-stu-id="f00a7-208">The following example shows the `Stop-AzureApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="f00a7-209">Cuando el estado de la puerta de enlace de aplicaciones sea detenido, use el cmdlet `Remove-AzureApplicationGateway` para quitar el servicio.</span><span class="sxs-lookup"><span data-stu-id="f00a7-209">Once the application gateway is in a stopped state, use the `Remove-AzureApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="f00a7-210">Para comprobar que se ha quitado el servicio, puede usar el cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="f00a7-210">To verify that the service has been removed, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="f00a7-211">Este paso no es necesario.</span><span class="sxs-lookup"><span data-stu-id="f00a7-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="f00a7-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f00a7-212">Next steps</span></span>

<span data-ttu-id="f00a7-213">Si desea configurar la descarga de SSL, consulte [Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante el modelo de implementación clásica](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f00a7-213">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="f00a7-214">Si quiere configurar una puerta de enlace de aplicaciones para usarla con el equilibrador de carga interno, consulte [Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="f00a7-214">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="f00a7-215">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="f00a7-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="f00a7-216">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="f00a7-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="f00a7-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="f00a7-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
