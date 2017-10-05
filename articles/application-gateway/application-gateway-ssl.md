---
title: "Configuración de la descarga SSL para Azure Application Gateway mediante el PowerShell clásico | Microsoft Docs"
description: "En este artículo se ofrecen instrucciones para crear una puerta de enlace de aplicaciones con descarga SSL mediante el modelo de implementación clásica de Azure."
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
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="82efc-103">Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="82efc-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="82efc-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="82efc-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="82efc-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="82efc-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="82efc-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="82efc-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="82efc-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="82efc-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="82efc-108">Azure Application Gateway puede configurarse para terminar la sesión Capa de sockets seguros (SSL) en la puerta de enlace para evitar las costosas tareas de descifrado SSL que tienen lugar en la granja de servidores web.</span><span class="sxs-lookup"><span data-stu-id="82efc-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="82efc-109">La descarga SSL también simplifica la configuración del servidor front-end y la administración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="82efc-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="82efc-110">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="82efc-110">Before you begin</span></span>

1. <span data-ttu-id="82efc-111">Instale la versión más reciente de los cmdlets de Azure PowerShell mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="82efc-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="82efc-112">Puede descargar e instalar la versión más reciente desde la sección **Windows PowerShell** de la página [Descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="82efc-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="82efc-113">Compruebe que tiene una red virtual de trabajo con una subred válida.</span><span class="sxs-lookup"><span data-stu-id="82efc-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="82efc-114">Asegúrese de que ninguna máquina virtual o implementación en la nube usan la subred.</span><span class="sxs-lookup"><span data-stu-id="82efc-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="82efc-115">La Puerta de enlace de aplicaciones debe encontrarse en una subred de red virtual.</span><span class="sxs-lookup"><span data-stu-id="82efc-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="82efc-116">Los servidores que configure para que usen la Puerta de enlace de aplicaciones deben existir, o bien sus puntos de conexión deben haberse creado en la red virtual o tener una dirección IP/VIP pública asignada.</span><span class="sxs-lookup"><span data-stu-id="82efc-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="82efc-117">Para configurar la descarga SSL en una puerta de enlace de aplicaciones, realice los pasos siguientes en el orden mostrado:</span><span class="sxs-lookup"><span data-stu-id="82efc-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="82efc-118">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="82efc-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="82efc-119">Carga de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="82efc-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="82efc-120">Configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="82efc-121">Establecimiento de la configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="82efc-122">Inicio de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="82efc-123">Comprobación del estado de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="82efc-124">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="82efc-124">Create an application gateway</span></span>

<span data-ttu-id="82efc-125">Para crear la puerta de enlace, use el cmdlet `New-AzureApplicationGateway` y reemplace los valores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="82efc-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="82efc-126">La facturación de la puerta de enlace no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="82efc-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="82efc-127">La facturación comienza en un paso posterior, cuando la puerta de enlace se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="82efc-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="82efc-128">Para validar la creación de la puerta de enlace, puede usar el cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="82efc-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="82efc-129">En el ejemplo, *Description*, *InstanceCount* y *GatewaySize* son parámetros opcionales.</span><span class="sxs-lookup"><span data-stu-id="82efc-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="82efc-130">El valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="82efc-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="82efc-131">El valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="82efc-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="82efc-132">Small y Large son otros valores disponibles.</span><span class="sxs-lookup"><span data-stu-id="82efc-132">Small and Large are other available values.</span></span> <span data-ttu-id="82efc-133">*VirtualIPs* y *DnsName* se muestran en blanco porque todavía no se ha iniciado la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="82efc-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="82efc-134">Estos valores se crearán una vez que la puerta de enlace esté en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="82efc-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="82efc-135">Carga de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="82efc-135">Upload SSL certificates</span></span>

<span data-ttu-id="82efc-136">Use `Add-AzureApplicationGatewaySslCertificate` para cargar el certificado de servidor en formato *pfx* en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82efc-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="82efc-137">El nombre del certificado es un nombre elegido por el usuario y debe ser único dentro de la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82efc-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="82efc-138">Este certificado se conoce con este nombre en todas las operaciones de administración de certificados en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82efc-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="82efc-139">En el ejemplo siguiente se muestra el cmdlet; reemplace los valores del ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="82efc-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="82efc-140">A continuación, valide la carga del certificado.</span><span class="sxs-lookup"><span data-stu-id="82efc-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="82efc-141">Utilice el cmdlet `Get-AzureApplicationGatewayCertificate` .</span><span class="sxs-lookup"><span data-stu-id="82efc-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="82efc-142">Este ejemplo muestra el cmdlet en la primera línea, seguido de la salida.</span><span class="sxs-lookup"><span data-stu-id="82efc-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

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
> <span data-ttu-id="82efc-143">La contraseña del certificado debe tener entre 4 y 12 caracteres, letras o números.</span><span class="sxs-lookup"><span data-stu-id="82efc-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="82efc-144">No se aceptan caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="82efc-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="82efc-145">Configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-145">Configure the gateway</span></span>

<span data-ttu-id="82efc-146">Una configuración de puerta de enlace de aplicaciones consta de varios valores.</span><span class="sxs-lookup"><span data-stu-id="82efc-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="82efc-147">Los valores pueden ir juntos para construir la configuración.</span><span class="sxs-lookup"><span data-stu-id="82efc-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="82efc-148">Los valores son:</span><span class="sxs-lookup"><span data-stu-id="82efc-148">The values are:</span></span>

* <span data-ttu-id="82efc-149">**Grupo de servidores back-end** : lista de direcciones IP de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="82efc-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="82efc-150">Las direcciones IP que se enumeran deben pertenecer a la subred de la red virtual o ser una IP/VIP pública.</span><span class="sxs-lookup"><span data-stu-id="82efc-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="82efc-151">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="82efc-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="82efc-152">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="82efc-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="82efc-153">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82efc-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="82efc-154">El tráfico llega a este puerto y después se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="82efc-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="82efc-155">**Agente de escucha** : tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="82efc-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="82efc-156">**Regla** : enlaza el agente de escucha y el grupo de servidores back-end y define a qué grupo de servidores back-end se dirigirá el tráfico cuando llega a un agente de escucha concreto.</span><span class="sxs-lookup"><span data-stu-id="82efc-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="82efc-157">Actualmente, solo se admite la regla *básica* .</span><span class="sxs-lookup"><span data-stu-id="82efc-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="82efc-158">La regla *básica* es la distribución de carga round robin.</span><span class="sxs-lookup"><span data-stu-id="82efc-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="82efc-159">**Notas de configuración adicionales**</span><span class="sxs-lookup"><span data-stu-id="82efc-159">**Additional configuration notes**</span></span>

<span data-ttu-id="82efc-160">Para la configuración de certificados SSL, el protocolo de **HttpListener** debería cambiar a *Https* (con distinción entre mayúsculas y minúsculas).</span><span class="sxs-lookup"><span data-stu-id="82efc-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="82efc-161">El elemento **SslCert** se agrega al elemento **HttpListener** con el valor establecido en el mismo nombre que se usa en la carga de la sección de certificados SSL anterior.</span><span class="sxs-lookup"><span data-stu-id="82efc-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="82efc-162">El puerto front-end debe actualizarse al 443.</span><span class="sxs-lookup"><span data-stu-id="82efc-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="82efc-163">**Para habilitar la afinidad basada en cookies**: se puede configurar una puerta de enlace de aplicaciones para asegurarse de que las solicitudes de una sesión de cliente siempre se dirigen a la misma máquina virtual de la granja de servidores web.</span><span class="sxs-lookup"><span data-stu-id="82efc-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="82efc-164">Este escenario se realiza mediante la inyección de una cookie de la sesión que permita a la puerta de enlace dirigir el tráfico de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="82efc-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="82efc-165">Para habilitar la afinidad basada en cookies, establezca **CookieBasedAffinity** en *Habilitado* en el elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="82efc-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="82efc-166">Puede llevar a cabo la configuración mediante la creación de un objeto de configuración o usando un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="82efc-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="82efc-167">Para llevar a cabo la configuración con un archivo XML de configuración, use el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="82efc-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="82efc-168">**Ejemplo XML de configuración**</span><span class="sxs-lookup"><span data-stu-id="82efc-168">**Configuration XML sample**</span></span>

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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="82efc-169">Establecimiento de la configuración de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-169">Set the gateway configuration</span></span>

<span data-ttu-id="82efc-170">A continuación, establecerá la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82efc-170">Next, you set the application gateway.</span></span> <span data-ttu-id="82efc-171">Puede usar el cmdlet `Set-AzureApplicationGatewayConfig` con un objeto de configuración o con un archivo XML de configuración.</span><span class="sxs-lookup"><span data-stu-id="82efc-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="82efc-172">Inicio de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-172">Start the gateway</span></span>

<span data-ttu-id="82efc-173">Una vez configurada la puerta de enlace, use el cmdlet `Start-AzureApplicationGateway` para iniciarla.</span><span class="sxs-lookup"><span data-stu-id="82efc-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="82efc-174">La facturación de una puerta de enlace de aplicaciones comienza después de que se haya iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="82efc-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="82efc-175">La regla `Start-AzureApplicationGateway` puede tardar hasta 15-20 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="82efc-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="82efc-176">Comprobación del estado de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="82efc-176">Verify the gateway status</span></span>

<span data-ttu-id="82efc-177">Use el cmdlet `Get-AzureApplicationGateway` para comprobar el estado de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="82efc-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="82efc-178">Si el cmdlet `Start-AzureApplicationGateway` se ha realizado correctamente en el paso anterior, el valor de *State* debería ser Running (En ejecución), y *VirtualIPs* y *DnsName* necesitan tener entradas válidas.</span><span class="sxs-lookup"><span data-stu-id="82efc-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="82efc-179">Este ejemplo muestra una puerta de enlace de aplicaciones que está operativa, en ejecución y lista para asumir el tráfico.</span><span class="sxs-lookup"><span data-stu-id="82efc-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="82efc-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82efc-180">Next steps</span></span>

<span data-ttu-id="82efc-181">Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:</span><span class="sxs-lookup"><span data-stu-id="82efc-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="82efc-182">Equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="82efc-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="82efc-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="82efc-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

