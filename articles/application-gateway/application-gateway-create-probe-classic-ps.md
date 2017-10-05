---
title: "Creación de un sondeo personalizado para Azure Application Gateway mediante PowerShell clásico | Microsoft Docs"
description: "Aprenda a crear un sondeo personalizado para la puerta de enlace de aplicaciones mediante PowerShell en el modelo de implementación clásica."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="61d2a-103">Creación de un sondeo personalizado para la Puerta de enlace de aplicaciones de Azure (clásica) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d2a-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="61d2a-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="61d2a-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="61d2a-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61d2a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="61d2a-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d2a-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="61d2a-107">En este artículo, agregará un sondeo personalizado a una puerta de enlace de aplicaciones existente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61d2a-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="61d2a-108">Los sondeos personalizados son útiles para aplicaciones que tienen una página de comprobación del estado o para aplicaciones que no proporcionan una respuesta correcta en la aplicación web predeterminada.</span><span class="sxs-lookup"><span data-stu-id="61d2a-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61d2a-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="61d2a-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="61d2a-110">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="61d2a-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="61d2a-111">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="61d2a-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="61d2a-112">Obtenga información sobre cómo [realizar estos pasos con el modelo de Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="61d2a-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="61d2a-113">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="61d2a-113">Create an application gateway</span></span>

<span data-ttu-id="61d2a-114">Para crear una Puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="61d2a-114">To create an application gateway:</span></span>

1. <span data-ttu-id="61d2a-115">Cree un recurso de Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="61d2a-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="61d2a-116">Cree un archivo de configuración XML o un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="61d2a-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="61d2a-117">Confirme la configuración para el recurso de la Puerta de enlace de aplicaciones recién creado.</span><span class="sxs-lookup"><span data-stu-id="61d2a-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="61d2a-118">Creación de un recurso de puerta de enlace de aplicaciones con un sondeo personalizado</span><span class="sxs-lookup"><span data-stu-id="61d2a-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="61d2a-119">Para crear la puerta de enlace, use el cmdlet `New-AzureApplicationGateway` y reemplace los valores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="61d2a-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="61d2a-120">La facturación de la puerta de enlace no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="61d2a-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="61d2a-121">La facturación comienza en un paso posterior, cuando la puerta de enlace se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="61d2a-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="61d2a-122">En el ejemplo siguiente se crea una puerta de enlace de aplicaciones nueva mediante una red virtual denominada testvnet1 y una subred llamada subnet-1.</span><span class="sxs-lookup"><span data-stu-id="61d2a-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="61d2a-123">Para validar la creación de la puerta de enlace, puede usar el cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="61d2a-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="61d2a-124">El valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="61d2a-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="61d2a-125">El valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="61d2a-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="61d2a-126">Puede elegir entre Pequeño, Mediano y Grande.</span><span class="sxs-lookup"><span data-stu-id="61d2a-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="61d2a-127">*VirtualIPs* y *DnsName* se muestran en blanco porque todavía no se ha iniciado la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="61d2a-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="61d2a-128">Estos valores se crearán una vez que la puerta de enlace esté en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="61d2a-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="61d2a-129">Configuración de una puerta de enlace de aplicaciones mediante XML</span><span class="sxs-lookup"><span data-stu-id="61d2a-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="61d2a-130">En el ejemplo siguiente, se usa un archivo XML para configurar todos los valores de la puerta de enlace de aplicaciones y confirmarlos en el recurso de dicha puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="61d2a-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="61d2a-131">Copie el texto siguiente y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="61d2a-131">Copy the following text to Notepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="61d2a-132">Edite los valores entre paréntesis de los elementos de configuración.</span><span class="sxs-lookup"><span data-stu-id="61d2a-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="61d2a-133">Guarde el archivo con extensión .xml.</span><span class="sxs-lookup"><span data-stu-id="61d2a-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="61d2a-134">En el ejemplo siguiente se muestra cómo usar un archivo de configuración para configurar la puerta de enlace de aplicaciones para que equilibre la carga de tráfico HTTP en el puerto público 80 y envíe el tráfico de red al puerto back-end 80 entre dos direcciones IP mediante sondeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="61d2a-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61d2a-135">El elemento de protocolo Http o Https distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="61d2a-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="61d2a-136">Se agrega un nuevo elemento de configuración \<Probe\> para configurar sondeos personalizados.</span><span class="sxs-lookup"><span data-stu-id="61d2a-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="61d2a-137">Los parámetros de configuración son:</span><span class="sxs-lookup"><span data-stu-id="61d2a-137">The configuration parameters are:</span></span>

|<span data-ttu-id="61d2a-138">Parámetro</span><span class="sxs-lookup"><span data-stu-id="61d2a-138">Parameter</span></span>|<span data-ttu-id="61d2a-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="61d2a-139">Description</span></span>|
|---|---|
|<span data-ttu-id="61d2a-140">**Name**</span><span class="sxs-lookup"><span data-stu-id="61d2a-140">**Name**</span></span> |<span data-ttu-id="61d2a-141">Nombre de referencia del sondeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="61d2a-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="61d2a-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="61d2a-142">* **Protocol**</span></span> | <span data-ttu-id="61d2a-143">Protocolo usado (los valores posibles son HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="61d2a-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="61d2a-144">**Host** y **Path**</span><span class="sxs-lookup"><span data-stu-id="61d2a-144">**Host** and **Path**</span></span> | <span data-ttu-id="61d2a-145">Dirección URL completa que invoca la puerta de enlace de aplicaciones para determinar el mantenimiento de la instancia.</span><span class="sxs-lookup"><span data-stu-id="61d2a-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="61d2a-146">Por ejemplo, si tiene el sitio web http://contoso.com/, el sondeo personalizado se puede configurar para "http://contoso.com/path/custompath.htm", con el fin de que las comprobaciones del sondeo tengan una respuesta HTTP satisfactoria.</span><span class="sxs-lookup"><span data-stu-id="61d2a-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="61d2a-147">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="61d2a-147">**Interval**</span></span> | <span data-ttu-id="61d2a-148">Configura las comprobaciones de intervalo de sondeo en segundos.</span><span class="sxs-lookup"><span data-stu-id="61d2a-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="61d2a-149">**Tiempo de espera**</span><span class="sxs-lookup"><span data-stu-id="61d2a-149">**Timeout**</span></span> | <span data-ttu-id="61d2a-150">Define el tiempo de espera de sondeo para una comprobación de respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="61d2a-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="61d2a-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="61d2a-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="61d2a-152">El número de respuestas HTTP con error que es necesario para marcar la instancia del back-end como *incorrecta*.</span><span class="sxs-lookup"><span data-stu-id="61d2a-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="61d2a-153">Se hace referencia al nombre del sondeo en la configuración de \<BackendHttpSettings\> para asignar el grupo de back-end que usará la configuración de sondeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="61d2a-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="61d2a-154">Adición de un sondeo personalizado a una puerta de enlace de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="61d2a-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="61d2a-155">El cambio de la configuración actual de una puerta de enlace de aplicaciones requiere tres pasos: obtener el archivo de configuración XML actual, modificarlo para que tenga un sondeo personalizado y configurar la puerta de enlace de aplicaciones con la nueva configuración XML.</span><span class="sxs-lookup"><span data-stu-id="61d2a-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="61d2a-156">Obtenga el archivo XML mediante `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="61d2a-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="61d2a-157">De esta forma, el cmdlet exportará el XML de configuración que se debe modificar para agregar una configuración de sondeo.</span><span class="sxs-lookup"><span data-stu-id="61d2a-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="61d2a-158">Abra el archivo XML en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="61d2a-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="61d2a-159">Agregue una sección `<probe>` después de `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="61d2a-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="61d2a-160">En la sección backendHttpSettings del XML, agregue el nombre del sondeo tal y como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61d2a-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="61d2a-161">Guarde el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="61d2a-161">Save the XML file.</span></span>

1. <span data-ttu-id="61d2a-162">Actualice la configuración de la instancia de Application Gateway con el nuevo archivo XML mediante `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="61d2a-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="61d2a-163">De esta forma, el cmdlet actualizará la instancia de Application Gateway con la nueva configuración.</span><span class="sxs-lookup"><span data-stu-id="61d2a-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="61d2a-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61d2a-164">Next steps</span></span>

<span data-ttu-id="61d2a-165">Si quiere configurar la descarga de Capa de sockets seguros (SSL), vea [Configure an application gateway for SSL offload](application-gateway-ssl.md)(Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante el modelo de implementación clásica).</span><span class="sxs-lookup"><span data-stu-id="61d2a-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="61d2a-166">Si quiere configurar una puerta de enlace de aplicaciones para usarla con el equilibrador de carga interno, consulte [Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="61d2a-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

