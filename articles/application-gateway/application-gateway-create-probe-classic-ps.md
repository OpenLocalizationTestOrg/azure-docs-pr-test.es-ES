---
title: "aaaCreate un clásico de PowerShell de sondeo personalizado - puerta de enlace de aplicaciones de Azure - | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate personalizado de sondeo para puerta de enlace de aplicaciones mediante el uso de PowerShell en el modelo de implementación clásica de Hola"
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
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="37b37-103">Creación de un sondeo personalizado para la Puerta de enlace de aplicaciones de Azure (clásica) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="37b37-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="37b37-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="37b37-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="37b37-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="37b37-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="37b37-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="37b37-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="37b37-107">En este artículo, se agregará un sondeo personalizado tooan aplicación puerta de enlace existente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37b37-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="37b37-108">Sondeos personalizados son útiles para las aplicaciones que tienen una página de comprobación de mantenimiento específico o para aplicaciones que no proporcionan una respuesta correcta en la aplicación web de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="37b37-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37b37-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="37b37-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="37b37-110">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="37b37-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="37b37-111">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="37b37-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="37b37-112">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="37b37-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="37b37-113">Creación de una puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="37b37-113">Create an application gateway</span></span>

<span data-ttu-id="37b37-114">toocreate una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="37b37-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="37b37-115">Cree un recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="37b37-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="37b37-116">Cree un archivo de configuración XML o un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="37b37-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="37b37-117">Confirmar Hola configuración toohello recién creado recursos de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="37b37-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="37b37-118">Creación de un recurso de puerta de enlace de aplicaciones con un sondeo personalizado</span><span class="sxs-lookup"><span data-stu-id="37b37-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="37b37-119">puerta de enlace de toocreate hello, use hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="37b37-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="37b37-120">La facturación de puerta de enlace de hello no se inicia en este momento.</span><span class="sxs-lookup"><span data-stu-id="37b37-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="37b37-121">Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.</span><span class="sxs-lookup"><span data-stu-id="37b37-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="37b37-122">Hello en el ejemplo siguiente se crea una puerta de enlace de la aplicación mediante el uso de una red virtual denominada "testvnet1" y una subred denominada "subred-1".</span><span class="sxs-lookup"><span data-stu-id="37b37-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="37b37-123">se creó toovalidate que Hola puerta de enlace, puede usar hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="37b37-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="37b37-124">Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="37b37-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="37b37-125">Hola valor predeterminado de *GatewaySize* es Medium.</span><span class="sxs-lookup"><span data-stu-id="37b37-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="37b37-126">Puede elegir entre Pequeño, Mediano y Grande.</span><span class="sxs-lookup"><span data-stu-id="37b37-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="37b37-127">*VirtualIPs* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="37b37-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="37b37-128">Estos valores se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="37b37-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="37b37-129">Configuración de una puerta de enlace de aplicaciones mediante XML</span><span class="sxs-lookup"><span data-stu-id="37b37-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="37b37-130">En el siguiente ejemplo de Hola, utilice un tooconfigure de archivo XML todos los valores de puerta de enlace de la aplicación y, a continuación, confirmarlos toohello de recursos de puerta de enlace de aplicación.</span><span class="sxs-lookup"><span data-stu-id="37b37-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="37b37-131">Copie Hola después tooNotepad de texto.</span><span class="sxs-lookup"><span data-stu-id="37b37-131">Copy hello following text tooNotepad.</span></span>

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

<span data-ttu-id="37b37-132">Editar valores de hello entre paréntesis Hola Hola elementos de configuración.</span><span class="sxs-lookup"><span data-stu-id="37b37-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="37b37-133">Guarde el archivo hello con extensión .xml.</span><span class="sxs-lookup"><span data-stu-id="37b37-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="37b37-134">Hello en el ejemplo siguiente se muestra cómo toouse una tooset de archivo de configuración de tooload de puerta de enlace de aplicación Hola equilibrar el tráfico HTTP en el puerto público 80 y enviar tráfico de red en el puerto 80 de final de tooback entre dos direcciones IP mediante el uso de un sondeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="37b37-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37b37-135">elemento de Hello protocolo Http o Https distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="37b37-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="37b37-136">Un nuevo elemento de configuración \<sondeo\> se agrega tooconfigure personalizado sondeos.</span><span class="sxs-lookup"><span data-stu-id="37b37-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="37b37-137">parámetros de configuración de Hello son:</span><span class="sxs-lookup"><span data-stu-id="37b37-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="37b37-138">Parámetro</span><span class="sxs-lookup"><span data-stu-id="37b37-138">Parameter</span></span>|<span data-ttu-id="37b37-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="37b37-139">Description</span></span>|
|---|---|
|<span data-ttu-id="37b37-140">**Name**</span><span class="sxs-lookup"><span data-stu-id="37b37-140">**Name**</span></span> |<span data-ttu-id="37b37-141">Nombre de referencia del sondeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="37b37-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="37b37-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="37b37-142">* **Protocol**</span></span> | <span data-ttu-id="37b37-143">Protocolo usado (los valores posibles son HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="37b37-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="37b37-144">**Host** y **Path**</span><span class="sxs-lookup"><span data-stu-id="37b37-144">**Host** and **Path**</span></span> | <span data-ttu-id="37b37-145">Escriba la ruta de acceso de dirección URL que se invoca con el estado hello toodetermine de puerta de enlace de aplicaciones de Hola de instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="37b37-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="37b37-146">Por ejemplo, si tiene un sitio Web http://contoso.com/, a continuación, el sondeo personalizado Hola puede configurarse para "http://contoso.com/path/custompath.htm" para la sonda comprueba toohave una respuesta HTTP correcta.</span><span class="sxs-lookup"><span data-stu-id="37b37-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="37b37-147">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="37b37-147">**Interval**</span></span> | <span data-ttu-id="37b37-148">Configura las comprobaciones de intervalo de sondeo de hello en segundos.</span><span class="sxs-lookup"><span data-stu-id="37b37-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="37b37-149">**Tiempo de espera**</span><span class="sxs-lookup"><span data-stu-id="37b37-149">**Timeout**</span></span> | <span data-ttu-id="37b37-150">Define el tiempo de espera de sondeo de Hola para una comprobación de la respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="37b37-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="37b37-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="37b37-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="37b37-152">Hola número de respuestas error HTTP necesario tooflag Hola back-end de la instancia como *incorrecto*.</span><span class="sxs-lookup"><span data-stu-id="37b37-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="37b37-153">nombre del sondeo Hola se hace referencia en hello \<BackendHttpSettings\> tooassign configuración qué grupo back-end utiliza la configuración de sondeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="37b37-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="37b37-154">Agregar un sondeo personalizado tooan aplicación puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="37b37-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="37b37-155">Cambiar la configuración actual Hola de una puerta de enlace de la aplicación requiere tres pasos: obtener el archivo de configuración XML actual hello, modificar toohave un sondeo personalizado y configurar puerta de enlace de aplicaciones de hello con una nueva configuración de XML Hola.</span><span class="sxs-lookup"><span data-stu-id="37b37-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="37b37-156">Obtener el archivo XML de hello mediante `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="37b37-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="37b37-157">Esta toobe XML de configuración de cmdlet exportaciones Hola había modificado tooadd una configuración de sondeo.</span><span class="sxs-lookup"><span data-stu-id="37b37-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="37b37-158">Abra el archivo XML de hello en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="37b37-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="37b37-159">Agregue una sección `<probe>` después de `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="37b37-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="37b37-160">En sección de backendHttpSettings de Hola de hello XML, agregue el nombre del sondeo de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="37b37-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

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

  <span data-ttu-id="37b37-161">Guarde el archivo XML de hello.</span><span class="sxs-lookup"><span data-stu-id="37b37-161">Save hello XML file.</span></span>

1. <span data-ttu-id="37b37-162">Configuración de puerta de enlace de la aplicación de actualización Hola con el nuevo archivo XML hello mediante el uso de `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="37b37-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="37b37-163">Este cmdlet actualiza la puerta de enlace de la aplicación con una nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="37b37-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="37b37-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37b37-164">Next steps</span></span>

<span data-ttu-id="37b37-165">Si desea que tooconfigure la descarga de capa de Sockets seguros (SSL), consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="37b37-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="37b37-166">Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno, consulte [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="37b37-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

