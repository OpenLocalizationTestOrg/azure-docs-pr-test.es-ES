---
title: "aaaConfigure SSL descargar PowerShell - puerta de enlace de aplicaciones de Azure - clásico | Documentos de Microsoft"
description: "Este artículo proporciona instrucciones toocreate descargar usando una puerta de enlace de la aplicación con SSL Hola modelo de implementación clásico de Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="dd258-103">Configurar una puerta de enlace de la aplicación para la descarga SSL mediante el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="dd258-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd258-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="dd258-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="dd258-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="dd258-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="dd258-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd258-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="dd258-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dd258-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="dd258-108">Puerta de enlace de aplicación de Azure puede ser configurado tooterminate Hola Secure Sockets Layer (SSL) sesión en hello puerta de enlace tooavoid costoso SSL descifrado tareas toohappen en la granja de servidores de hello web.</span><span class="sxs-lookup"><span data-stu-id="dd258-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="dd258-109">Descarga SSL también simplifica la administración de aplicación web de Hola y el programa de instalación del servidor front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dd258-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="dd258-110">Before you begin</span></span>

1. <span data-ttu-id="dd258-111">Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="dd258-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="dd258-112">Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dd258-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dd258-113">Compruebe que tiene una red virtual de trabajo con una subred válida.</span><span class="sxs-lookup"><span data-stu-id="dd258-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="dd258-114">Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="dd258-115">puerta de enlace de aplicaciones de Hello debe ser por sí solo en una subred de red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd258-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="dd258-116">deben existir servidores Hola configurar la puerta de enlace de aplicaciones de toouse Hola o tener asignados de sus puntos de conexión creados en la red virtual de Hola o con una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="dd258-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="dd258-117">tooconfigure SSL descargar en una puerta de enlace de aplicaciones, Hola siguiendo los pasos en orden de hello mostrado:</span><span class="sxs-lookup"><span data-stu-id="dd258-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="dd258-118">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="dd258-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="dd258-119">Carga de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="dd258-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="dd258-120">Configurar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd258-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="dd258-121">Configuración de puerta de enlace de Hola de conjunto</span><span class="sxs-lookup"><span data-stu-id="dd258-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="dd258-122">Iniciar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd258-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="dd258-123">Comprobar el estado de la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd258-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="dd258-124">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="dd258-124">Create an application gateway</span></span>

<span data-ttu-id="dd258-125">puerta de enlace de toocreate hello, use hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="dd258-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="dd258-126">La facturación de puerta de enlace de hello no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="dd258-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="dd258-127">Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="dd258-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="dd258-128">se creó toovalidate que Hola puerta de enlace, puede usar hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dd258-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="dd258-129">En el ejemplo de Hola, *descripción*, *InstanceCount*, y *GatewaySize* son parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="dd258-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="dd258-130">Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="dd258-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="dd258-131">Hola valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="dd258-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="dd258-132">Small y Large son otros valores disponibles.</span><span class="sxs-lookup"><span data-stu-id="dd258-132">Small and Large are other available values.</span></span> <span data-ttu-id="dd258-133">*VirtualIPs* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="dd258-134">Estos valores se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="dd258-135">Carga de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="dd258-135">Upload SSL certificates</span></span>

<span data-ttu-id="dd258-136">Use `Add-AzureApplicationGatewaySslCertificate` certificado de servidor hello tooupload en *pfx* puerta de enlace de aplicaciones de toohello de formato.</span><span class="sxs-lookup"><span data-stu-id="dd258-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="dd258-137">nombre del certificado Hello es un nombre elegido por el usuario y debe ser único dentro de la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="dd258-138">Este certificado es tooby que se hace referencia este nombre en todas las operaciones de administración de certificados en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="dd258-139">Este ejemplo siguiente muestra el cmdlet de hello, reemplazar valores de hello en el ejemplo de Hola por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="dd258-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="dd258-140">A continuación, validar la carga del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="dd258-141">Hola de uso `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dd258-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="dd258-142">Ejemplo hello cmdlet muestra en la primera línea hello, seguido de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="dd258-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="dd258-143">contraseña del certificado Hello tiene toobe entre 4 too12 caracteres, letras o números.</span><span class="sxs-lookup"><span data-stu-id="dd258-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="dd258-144">No se aceptan caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="dd258-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="dd258-145">Configurar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd258-145">Configure hello gateway</span></span>

<span data-ttu-id="dd258-146">Una configuración de puerta de enlace de aplicaciones consta de varios valores.</span><span class="sxs-lookup"><span data-stu-id="dd258-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="dd258-147">se pueden acumular los valores de Hello configuración de hello tooconstruct juntos.</span><span class="sxs-lookup"><span data-stu-id="dd258-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="dd258-148">los valores de Hello son:</span><span class="sxs-lookup"><span data-stu-id="dd258-148">hello values are:</span></span>

* <span data-ttu-id="dd258-149">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="dd258-150">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="dd258-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="dd258-151">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="dd258-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="dd258-152">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="dd258-153">**Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="dd258-154">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="dd258-155">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="dd258-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="dd258-156">**Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="dd258-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="dd258-157">Actualmente, solo Hola *básico* se admite la regla.</span><span class="sxs-lookup"><span data-stu-id="dd258-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="dd258-158">Hola *básica* regla es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="dd258-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="dd258-159">**Notas de configuración adicionales**</span><span class="sxs-lookup"><span data-stu-id="dd258-159">**Additional configuration notes**</span></span>

<span data-ttu-id="dd258-160">Para la configuración de certificados SSL, Hola protocolo en **HttpListener** debe cambiar también*Https* (con distinción entre mayúsculas y minúsculas).</span><span class="sxs-lookup"><span data-stu-id="dd258-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="dd258-161">Hola **SslCert** elemento se agrega demasiado**HttpListener** con hello valor establecido toohello mismo nombre tal y como se utiliza en la carga de Hola de sección de certificados SSL anterior.</span><span class="sxs-lookup"><span data-stu-id="dd258-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="dd258-162">puerto front-end de Hello deben too443 actualizada.</span><span class="sxs-lookup"><span data-stu-id="dd258-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="dd258-163">**tooenable basado en cookies afinidad**: una puerta de enlace de la aplicación puede ser configurado tooensure que una solicitud de una sesión de cliente siempre está dirigido toohello misma máquina virtual en la granja de servidores de hello web.</span><span class="sxs-lookup"><span data-stu-id="dd258-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="dd258-164">Este escenario se realiza mediante la inyección de una cookie de sesión que permita el tráfico de toodirect de puerta de enlace de hello adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="dd258-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="dd258-165">establece la afinidad basado en cookies tooenable, **CookieBasedAffinity** demasiado*habilitado* en hello **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="dd258-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="dd258-166">Puede llevar a cabo la configuración mediante la creación de un objeto de configuración o usando un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="dd258-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="dd258-167">usar la configuración mediante el uso de una archivo XML de configuración de tooconstruct Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dd258-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="dd258-168">**Ejemplo XML de configuración**</span><span class="sxs-lookup"><span data-stu-id="dd258-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="dd258-169">Configuración de puerta de enlace de Hola de conjunto</span><span class="sxs-lookup"><span data-stu-id="dd258-169">Set hello gateway configuration</span></span>

<span data-ttu-id="dd258-170">A continuación, configure la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="dd258-171">Puede usar hello `Set-AzureApplicationGatewayConfig` cmdlet con un objeto de configuración o con un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="dd258-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="dd258-172">Iniciar la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd258-172">Start hello gateway</span></span>

<span data-ttu-id="dd258-173">Una vez que se ha configurado la puerta de enlace de hello, usar hello `Start-AzureApplicationGateway` puerta de enlace de cmdlet toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="dd258-174">La facturación de una puerta de enlace de la aplicación comienza después de puerta de enlace de Hola se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="dd258-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="dd258-175">Hola `Start-AzureApplicationGateway` cmdlet podría tardar hasta toofinish too15-20 minutos.</span><span class="sxs-lookup"><span data-stu-id="dd258-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="dd258-176">Comprobar el estado de la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd258-176">Verify hello gateway status</span></span>

<span data-ttu-id="dd258-177">Hola de uso `Get-AzureApplicationGateway` estado de cmdlet toocheck Hola de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd258-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="dd258-178">Si `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior de hello, *estado* debe estar en ejecución, y *VirtualIPs* y *DnsName* debe tener las entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="dd258-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="dd258-179">Este ejemplo muestra una puerta de enlace de la aplicación que está activo, ejecutando y un tráfico tootake listo.</span><span class="sxs-lookup"><span data-stu-id="dd258-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="dd258-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd258-180">Next steps</span></span>

<span data-ttu-id="dd258-181">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="dd258-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="dd258-182">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="dd258-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="dd258-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="dd258-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

