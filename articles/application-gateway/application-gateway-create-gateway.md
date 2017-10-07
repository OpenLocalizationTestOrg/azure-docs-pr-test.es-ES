---
title: aaaCreate, iniciar o eliminar una puerta de enlace de aplicaciones | Documentos de Microsoft
description: "Esta página proporciona instrucciones toocreate, configurar, iniciar y eliminar una puerta de enlace de la aplicación de Azure"
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
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="c0d05-103">Creación, inicio o eliminación de una puerta de enlace de aplicaciones con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0d05-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0d05-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c0d05-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="c0d05-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c0d05-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="c0d05-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0d05-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="c0d05-107">Plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="c0d05-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="c0d05-108">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c0d05-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="c0d05-109">Azure Application Gateway es un equilibrador de carga de nivel 7.</span><span class="sxs-lookup"><span data-stu-id="c0d05-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="c0d05-110">Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local.</span><span class="sxs-lookup"><span data-stu-id="c0d05-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="c0d05-111">Application Gateway proporciona numerosas características del Controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, etc.</span><span class="sxs-lookup"><span data-stu-id="c0d05-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="c0d05-112">toofind una lista completa de las características admitidas, visite [información general sobre la puerta de enlace de aplicaciones](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c0d05-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="c0d05-113">Este artículo le guiará a través de hello pasos toocreate, configurar, iniciar y eliminar una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0d05-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0d05-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c0d05-114">Before you begin</span></span>

1. <span data-ttu-id="c0d05-115">Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="c0d05-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="c0d05-116">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c0d05-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c0d05-117">Si tiene una red virtual existente, seleccione una subred vacía existente o crear una nueva subred en la red virtual existente únicamente para su uso por la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="c0d05-118">No se puede implementar Hola aplicación puerta de enlace tooa red virtual diferente que los recursos de hello piensa toodeploy detrás de la puerta de enlace de aplicación Hola a menos que se utiliza el intercambio de tráfico de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c0d05-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="c0d05-119">toolearn más visite [intercambio de tráfico de red virtual](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c0d05-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="c0d05-120">Compruebe que tiene una red virtual de trabajo con una subred válida.</span><span class="sxs-lookup"><span data-stu-id="c0d05-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="c0d05-121">Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="c0d05-122">puerta de enlace de aplicaciones de Hello debe ser por sí solo en una subred de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c0d05-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="c0d05-123">deben existir servidores Hola configurar la puerta de enlace de aplicaciones de toouse Hola o tener asignados de sus puntos de conexión creados en la red virtual de Hola o con una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="c0d05-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="c0d05-124">¿Qué es necesario toocreate una puerta de enlace de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="c0d05-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="c0d05-125">Cuando usas hello `New-AzureApplicationGateway` comando toocreate Hola aplicación puerta de enlace, no se ha configurado en este momento y recursos Hola recién creada se configuran mediante XML o un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="c0d05-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="c0d05-126">los valores de Hello son:</span><span class="sxs-lookup"><span data-stu-id="c0d05-126">hello values are:</span></span>

* <span data-ttu-id="c0d05-127">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="c0d05-128">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="c0d05-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="c0d05-129">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="c0d05-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="c0d05-130">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="c0d05-131">**Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="c0d05-132">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="c0d05-133">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="c0d05-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="c0d05-134">**Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="c0d05-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="c0d05-135">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c0d05-135">Create an application gateway</span></span>

<span data-ttu-id="c0d05-136">toocreate una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="c0d05-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="c0d05-137">Cree un recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="c0d05-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="c0d05-138">Cree un archivo de configuración XML o un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="c0d05-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="c0d05-139">Confirmar Hola configuración toohello recién creado recursos de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c0d05-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d05-140">Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c0d05-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="c0d05-141">Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="c0d05-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Escenario de ejemplo][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="c0d05-143">Crear un recurso de la puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c0d05-143">Create an application gateway resource</span></span>

<span data-ttu-id="c0d05-144">puerta de enlace de toocreate hello, use hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="c0d05-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="c0d05-145">La facturación de puerta de enlace de hello no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="c0d05-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="c0d05-146">Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="c0d05-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="c0d05-147">Hello en el ejemplo siguiente se crea una puerta de enlace de la aplicación mediante el uso de una red virtual denominada "testvnet1" y una subred denominada "subred-1":</span><span class="sxs-lookup"><span data-stu-id="c0d05-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="c0d05-148">*Description*, *InstanceCount* y *GatewaySize* son parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="c0d05-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="c0d05-149">se creó toovalidate que Hola puerta de enlace, puede usar hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c0d05-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

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
> <span data-ttu-id="c0d05-150">Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="c0d05-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="c0d05-151">Hola valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="c0d05-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="c0d05-152">Puede elegir entre Pequeño, Mediano y Grande.</span><span class="sxs-lookup"><span data-stu-id="c0d05-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="c0d05-153">*VirtualIPs* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="c0d05-154">Estos se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="c0d05-155">Configurar la puerta de enlace de aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="c0d05-155">Configure hello application gateway</span></span>

<span data-ttu-id="c0d05-156">Puede configurar la puerta de enlace de aplicaciones de hello mediante el uso de XML o un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="c0d05-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="c0d05-157">Configurar la puerta de enlace de aplicaciones de hello mediante XML</span><span class="sxs-lookup"><span data-stu-id="c0d05-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="c0d05-158">En el siguiente ejemplo de Hola, utilice un tooconfigure de archivo XML todos los valores de puerta de enlace de la aplicación y, a continuación, confirmarlos toohello de recursos de puerta de enlace de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0d05-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="c0d05-159">Paso 1</span><span class="sxs-lookup"><span data-stu-id="c0d05-159">Step 1</span></span>

<span data-ttu-id="c0d05-160">Copie Hola después tooNotepad de texto.</span><span class="sxs-lookup"><span data-stu-id="c0d05-160">Copy hello following text tooNotepad.</span></span>

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

<span data-ttu-id="c0d05-161">Editar valores de hello entre paréntesis Hola Hola elementos de configuración.</span><span class="sxs-lookup"><span data-stu-id="c0d05-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="c0d05-162">Guarde el archivo hello con extensión .xml.</span><span class="sxs-lookup"><span data-stu-id="c0d05-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d05-163">elemento de Hello protocolo Http o Https distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c0d05-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="c0d05-164">Hola de ejemplo siguiente muestra cómo toouse una configuración de archivo tooset de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="c0d05-165">carga de ejemplo de Hola equilibra el tráfico HTTP en el puerto público 80 y envía el tráfico de red en el puerto 80 de final de tooback entre dos direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="c0d05-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

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

#### <a name="step-2"></a><span data-ttu-id="c0d05-166">Paso 2</span><span class="sxs-lookup"><span data-stu-id="c0d05-166">Step 2</span></span>

<span data-ttu-id="c0d05-167">A continuación, establezca la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-167">Next, set hello application gateway.</span></span> <span data-ttu-id="c0d05-168">Hola de uso `Set-AzureApplicationGatewayConfig` cmdlet con un archivo de configuración XML.</span><span class="sxs-lookup"><span data-stu-id="c0d05-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="c0d05-169">Configurar la puerta de enlace de aplicaciones de hello mediante el uso de un objeto de configuración</span><span class="sxs-lookup"><span data-stu-id="c0d05-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="c0d05-170">Hola de ejemplo siguiente muestra cómo tooconfigure Hola puerta de enlace de aplicaciones mediante el uso de objetos de configuración.</span><span class="sxs-lookup"><span data-stu-id="c0d05-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="c0d05-171">Todos los elementos de configuración deben configurarse individualmente y, a continuación, agregar objeto de configuración de puerta de enlace de tooan aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0d05-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="c0d05-172">Después de crear el objeto de configuración de hello, usar hello `Set-AzureApplicationGateway` comando toocommit Hola configuración toohello creado anteriormente recursos de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c0d05-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d05-173">Antes de asignar un objeto de configuración de tooeach de valor, debe toodeclare qué tipo de objeto de PowerShell que se usa para el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c0d05-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="c0d05-174">elementos individuales de Hello primera línea toocreate Hola define qué `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` se usan.</span><span class="sxs-lookup"><span data-stu-id="c0d05-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="c0d05-175">Paso 1</span><span class="sxs-lookup"><span data-stu-id="c0d05-175">Step 1</span></span>

<span data-ttu-id="c0d05-176">Cree todos los elementos de configuración individuales.</span><span class="sxs-lookup"><span data-stu-id="c0d05-176">Create all individual configuration items.</span></span>

<span data-ttu-id="c0d05-177">Cree la IP de front-end de hello tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="c0d05-178">Crear puertos front-end de hello tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="c0d05-179">Crear grupo de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="c0d05-180">Define las direcciones IP Hola que se agregan el grupo de servidores de back-end de toohello tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="c0d05-181">Utilice Hola $server object tooadd Hola valores toohello grupo back-end (objeto) ($pool).</span><span class="sxs-lookup"><span data-stu-id="c0d05-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="c0d05-182">Crear configuración de grupo de servidor back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="c0d05-183">Crear Agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="c0d05-184">Crear regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="c0d05-185">Paso 2</span><span class="sxs-lookup"><span data-stu-id="c0d05-185">Step 2</span></span>

<span data-ttu-id="c0d05-186">Asignar todas las configuración individual elementos tooan aplicación puerta de enlace configuración objeto ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="c0d05-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="c0d05-187">Agregar configuración de toohello IP front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="c0d05-188">Agregar configuración de toohello de hello puerto front-end.</span><span class="sxs-lookup"><span data-stu-id="c0d05-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="c0d05-189">Agregar configuración de toohello del grupo de servidor back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="c0d05-190">Agregue la configuración de toohello de configuración del grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="c0d05-191">Agregar configuración de toohello de agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="c0d05-192">Agregar configuración de la regla toohello Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="c0d05-193">Paso 3</span><span class="sxs-lookup"><span data-stu-id="c0d05-193">Step 3</span></span>
<span data-ttu-id="c0d05-194">Confirmar el recurso de puerta de enlace de aplicaciones de toohello objeto de configuración de hello utilizando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="c0d05-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="c0d05-195">Iniciar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="c0d05-195">Start hello gateway</span></span>

<span data-ttu-id="c0d05-196">Una vez que se ha configurado la puerta de enlace de hello, usar hello `Start-AzureApplicationGateway` puerta de enlace de cmdlet toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="c0d05-197">La facturación de una puerta de enlace de la aplicación comienza después de puerta de enlace de Hola se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="c0d05-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d05-198">Hola `Start-AzureApplicationGateway` cmdlet podría tardar hasta toofinish too15-20 minutos.</span><span class="sxs-lookup"><span data-stu-id="c0d05-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="c0d05-199">Comprobar el estado de la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="c0d05-199">Verify hello gateway status</span></span>

<span data-ttu-id="c0d05-200">Hola de uso `Get-AzureApplicationGateway` estado de cmdlet toocheck Hola de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="c0d05-201">Si `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior de hello, *estado* debe estar en ejecución, y *Vip* y *DnsName* debe tener las entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="c0d05-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="c0d05-202">Hello en el ejemplo siguiente se muestra una puerta de enlace de la aplicación que está en funcionamiento y en ejecución, y tootake listo tráfico destinado `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="c0d05-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="c0d05-203">Eliminar puerta de enlace de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="c0d05-203">Delete hello application gateway</span></span>

<span data-ttu-id="c0d05-204">puerta de enlace de aplicaciones de Hola toodelete:</span><span class="sxs-lookup"><span data-stu-id="c0d05-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="c0d05-205">Hola de uso `Stop-AzureApplicationGateway` puerta de enlace de cmdlet toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="c0d05-206">Hola de uso `Remove-AzureApplicationGateway` puerta de enlace de cmdlet tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="c0d05-207">Compruebe dicha puerta de enlace de Hola se ha eliminado mediante el uso de hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c0d05-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="c0d05-208">Hello en el ejemplo siguiente se muestra hello `Stop-AzureApplicationGateway` cmdlet en la primera línea hello, seguido de la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c0d05-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

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

<span data-ttu-id="c0d05-209">Una vez que la puerta de enlace de aplicaciones de hello está en estado detenido, use hello `Remove-AzureApplicationGateway` servicio de cmdlet tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="c0d05-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

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

<span data-ttu-id="c0d05-210">se ha quitado tooverify que Hola servicio, puede usar hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c0d05-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="c0d05-211">Este paso no es necesario.</span><span class="sxs-lookup"><span data-stu-id="c0d05-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="c0d05-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0d05-212">Next steps</span></span>

<span data-ttu-id="c0d05-213">Si desea que tooconfigure la descarga de SSL, consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="c0d05-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="c0d05-214">Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno, consulte [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="c0d05-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="c0d05-215">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="c0d05-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="c0d05-216">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="c0d05-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="c0d05-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c0d05-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
