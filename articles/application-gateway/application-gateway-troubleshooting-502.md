---
title: "errores de aplicación de Azure puerta de enlace Gateway incorrecta (502) aaaTroubleshoot | Documentos de Microsoft"
description: "Obtenga información acerca de cómo errores tootroubleshoot 502 de puerta de enlace de aplicaciones"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="57065-103">Solución de errores de puerta de enlace incorrecta en el servicio Puerta de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="57065-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="57065-104">Obtenga información acerca de cómo tootroubleshoot (502) (errores) puerta de enlace errónea reciben al usar la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="57065-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="57065-105">Información general</span><span class="sxs-lookup"><span data-stu-id="57065-105">Overview</span></span>

<span data-ttu-id="57065-106">Después de configurar una puerta de enlace de aplicaciones, uno de los errores de Hola que los usuarios pueden encontrar es "Error de servidor: 502: el servidor Web recibió una respuesta no válida mientras actuaba como un servidor de puerta de enlace o proxy".</span><span class="sxs-lookup"><span data-stu-id="57065-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="57065-107">Este error puede ocurrir debido toohello siguiente razones principales:</span><span class="sxs-lookup"><span data-stu-id="57065-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="57065-108">[El grupo back-end de la instancia de Azure Application Gateway no está configurado o está vacío](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="57065-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="57065-109">Ninguna de las máquinas virtuales de Hola o instancias de [conjunto de escalado de máquinas virtuales están en buen estado](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="57065-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="57065-110">Máquinas virtuales o instancias del conjunto de escalado de VM de back-end son [no responde sondeo de estado predeterminado de toohello](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="57065-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="57065-111">[La configuración de las sondas de estado personalizadas](#problems-with-custom-health-probe.md) no es válida o adecuada.</span><span class="sxs-lookup"><span data-stu-id="57065-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="57065-112">[El tiempo de espera de solicitud se superó o hay problemas de conectividad](#request-time-out) con las solicitudes de usuario.</span><span class="sxs-lookup"><span data-stu-id="57065-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="57065-113">Valor de BackendAddressPool vacío</span><span class="sxs-lookup"><span data-stu-id="57065-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="57065-114">Causa</span><span class="sxs-lookup"><span data-stu-id="57065-114">Cause</span></span>

<span data-ttu-id="57065-115">Si Hola puerta de enlace de aplicaciones no tiene ninguna máquina virtual o conjunto de escalado de VM configurada en el grupo de direcciones de back-end de hello, no se pueden enrutar cualquier solicitud de cliente y genera un error de puerta de enlace errónea.</span><span class="sxs-lookup"><span data-stu-id="57065-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="57065-116">Solución</span><span class="sxs-lookup"><span data-stu-id="57065-116">Solution</span></span>

<span data-ttu-id="57065-117">Asegúrese de que el grupo de direcciones de back-end de hello no está vacía.</span><span class="sxs-lookup"><span data-stu-id="57065-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="57065-118">Puede hacerlo mediante PowerShell, la CLI o el Portal.</span><span class="sxs-lookup"><span data-stu-id="57065-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="57065-119">salida de Hello de hello anterior cmdlet debe contener grupo de direcciones de back-end no está vacío.</span><span class="sxs-lookup"><span data-stu-id="57065-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="57065-120">A continuación, se muestra un ejemplo en el que se devuelven dos grupos que están configurados con direcciones IP o FQDN de máquinas virtuales de back-end.</span><span class="sxs-lookup"><span data-stu-id="57065-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="57065-121">Hola estado de aprovisionamiento de hello BackendAddressPool debe ser "realizado."</span><span class="sxs-lookup"><span data-stu-id="57065-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="57065-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="57065-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="57065-123">Instancias incorrectas en BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="57065-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="57065-124">Causa</span><span class="sxs-lookup"><span data-stu-id="57065-124">Cause</span></span>

<span data-ttu-id="57065-125">Si todas las instancias de Hola de BackendAddressPool tienen un estado incorrecto, puerta de enlace de aplicaciones no tendría cualquier solicitud de usuario tooroute de back-end.</span><span class="sxs-lookup"><span data-stu-id="57065-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="57065-126">También pueden caso hello cuando instancias de back-end están en buen Estados, pero no tiene la aplicación hello necesario implementada.</span><span class="sxs-lookup"><span data-stu-id="57065-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="57065-127">Solución</span><span class="sxs-lookup"><span data-stu-id="57065-127">Solution</span></span>

<span data-ttu-id="57065-128">Asegúrese de que las instancias de hello están en buen estadas y aplicación hello está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="57065-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="57065-129">Compruebe si hay instancias de back-end de hello toorespond pueda tooa ping desde otra máquina virtual de Hola misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="57065-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="57065-130">Si se configura con un punto de conexión público, asegúrese de que una aplicación web de explorador solicitud toohello es reparables por.</span><span class="sxs-lookup"><span data-stu-id="57065-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="57065-131">Problemas con la sonda de estado predeterminada</span><span class="sxs-lookup"><span data-stu-id="57065-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="57065-132">Causa</span><span class="sxs-lookup"><span data-stu-id="57065-132">Cause</span></span>

<span data-ttu-id="57065-133">502 (errores) también pueden ser indicadores frecuentes que Hola de sondeo de estado predeterminado es no se puede tooreach máquinas virtuales de back-end.</span><span class="sxs-lookup"><span data-stu-id="57065-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="57065-134">Cuando se aprovisiona una instancia de puerta de enlace de aplicaciones, se configura automáticamente un sondeo de estado predeterminado tooeach BackendAddressPool mediante las propiedades de hello BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="57065-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="57065-135">Ningún usuario de entrada se tooset requiere este sondeo.</span><span class="sxs-lookup"><span data-stu-id="57065-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="57065-136">En concreto, cuando se configura una regla de equilibrio de carga, se crea una asociación entre un elemento BackendHttpSetting y otro BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="57065-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="57065-137">Un sondeo predeterminado está configurado para cada una de estas asociaciones y una instancia de tooeach de conexión de comprobación de estado periódicas en Hola BackendAddressPool en hello el puerto especificado en el elemento de hello BackendHttpSetting inicia la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="57065-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="57065-138">Tabla siguiente enumera los valores de hello asociados de sondeo de estado de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="57065-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="57065-139">Propiedad de sondeo</span><span class="sxs-lookup"><span data-stu-id="57065-139">Probe property</span></span> | <span data-ttu-id="57065-140">Valor</span><span class="sxs-lookup"><span data-stu-id="57065-140">Value</span></span> | <span data-ttu-id="57065-141">Description</span><span class="sxs-lookup"><span data-stu-id="57065-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57065-142">Dirección URL de sondeo</span><span class="sxs-lookup"><span data-stu-id="57065-142">Probe URL</span></span> |<span data-ttu-id="57065-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="57065-143">http://127.0.0.1/</span></span> |<span data-ttu-id="57065-144">Ruta de acceso URL</span><span class="sxs-lookup"><span data-stu-id="57065-144">URL path</span></span> |
| <span data-ttu-id="57065-145">Intervalo</span><span class="sxs-lookup"><span data-stu-id="57065-145">Interval</span></span> |<span data-ttu-id="57065-146">30</span><span class="sxs-lookup"><span data-stu-id="57065-146">30</span></span> |<span data-ttu-id="57065-147">Intervalo de sondeo en segundos</span><span class="sxs-lookup"><span data-stu-id="57065-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="57065-148">Tiempo de espera</span><span class="sxs-lookup"><span data-stu-id="57065-148">Time-out</span></span> |<span data-ttu-id="57065-149">30</span><span class="sxs-lookup"><span data-stu-id="57065-149">30</span></span> |<span data-ttu-id="57065-150">Tiempo de espera del sondeo en segundos</span><span class="sxs-lookup"><span data-stu-id="57065-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="57065-151">Umbral incorrecto</span><span class="sxs-lookup"><span data-stu-id="57065-151">Unhealthy threshold</span></span> |<span data-ttu-id="57065-152">3</span><span class="sxs-lookup"><span data-stu-id="57065-152">3</span></span> |<span data-ttu-id="57065-153">Número de reintentos de sondeo.</span><span class="sxs-lookup"><span data-stu-id="57065-153">Probe retry count.</span></span> <span data-ttu-id="57065-154">servidor de back-end de Hola está marcado después de recuento de errores de sondeo consecutivos Hola alcanza el umbral de estado incorrecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="57065-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="57065-155">Solución</span><span class="sxs-lookup"><span data-stu-id="57065-155">Solution</span></span>

* <span data-ttu-id="57065-156">Asegúrese de que se ha configurado un sitio predeterminado y de que está escuchando en 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="57065-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="57065-157">Si BackendHttpSetting especifica un puerto distinto del 80, sitio predeterminado de hello debe ser toolisten configurado en ese puerto.</span><span class="sxs-lookup"><span data-stu-id="57065-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="57065-158">Hello toohttp://127.0.0.1:port de llamada debe devolver un código de resultado HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="57065-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="57065-159">Esto se debe devolver en tiempo de espera de 30 seg Hola.</span><span class="sxs-lookup"><span data-stu-id="57065-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="57065-160">Asegúrese de que el puerto configurado está abierto y que no existen reglas de firewall ni grupos de seguridad de red de Azure, que bloquee el tráfico entrante o saliente en el puerto de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="57065-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="57065-161">Si se usa máquinas virtuales de Azure clásicas o servicio en la nube con el FQDN o una dirección IP pública, asegúrese de que Hola correspondiente [extremo](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) se abre.</span><span class="sxs-lookup"><span data-stu-id="57065-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="57065-162">Si Hola máquina virtual se configura a través del Administrador de recursos de Azure y está fuera de la red virtual donde se implementa la puerta de enlace de aplicaciones, Hola [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) debe configurarse acceso tooallow en hello deseado puerto.</span><span class="sxs-lookup"><span data-stu-id="57065-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="57065-163">Problemas con la sonda de estado personalizada</span><span class="sxs-lookup"><span data-stu-id="57065-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="57065-164">Causa</span><span class="sxs-lookup"><span data-stu-id="57065-164">Cause</span></span>

<span data-ttu-id="57065-165">Sondeo de estado personalizados permite comportamiento de búsqueda predeterminadas de toohello de flexibilidad adicional.</span><span class="sxs-lookup"><span data-stu-id="57065-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="57065-166">Cuando se usa sondeos personalizados, los usuarios pueden configurar intervalo de sondeo de saludo, dirección URL de hello y tootest de ruta de acceso y cuántos tooaccept de respuestas error antes de marcar la instancia de grupo de servidores de back-end de hello como en mal estado.</span><span class="sxs-lookup"><span data-stu-id="57065-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="57065-167">Hola propiedades adicionales siguientes se agrega.</span><span class="sxs-lookup"><span data-stu-id="57065-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="57065-168">Propiedad de sondeo</span><span class="sxs-lookup"><span data-stu-id="57065-168">Probe property</span></span> | <span data-ttu-id="57065-169">Description</span><span class="sxs-lookup"><span data-stu-id="57065-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57065-170">Nombre</span><span class="sxs-lookup"><span data-stu-id="57065-170">Name</span></span> |<span data-ttu-id="57065-171">Nombre del sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57065-171">Name of hello probe.</span></span> <span data-ttu-id="57065-172">También se denomina sondeo de toohello toorefer usado en la configuración de HTTP de back-end.</span><span class="sxs-lookup"><span data-stu-id="57065-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="57065-173">Protocol</span><span class="sxs-lookup"><span data-stu-id="57065-173">Protocol</span></span> |<span data-ttu-id="57065-174">Usa el protocolo de sondeo de hello toosend.</span><span class="sxs-lookup"><span data-stu-id="57065-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="57065-175">sondeo de Hello usa el protocolo de hello definido en la configuración de HTTP de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="57065-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="57065-176">Host</span><span class="sxs-lookup"><span data-stu-id="57065-176">Host</span></span> |<span data-ttu-id="57065-177">Sondeo de Hola de toosend de nombre de host.</span><span class="sxs-lookup"><span data-stu-id="57065-177">Host name toosend hello probe.</span></span> <span data-ttu-id="57065-178">Solo es aplicable cuando se ha configurado un entorno multisitio en Puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="57065-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="57065-179">Es diferente al nombre de host de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57065-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="57065-180">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="57065-180">Path</span></span> |<span data-ttu-id="57065-181">Ruta de acceso relativa del sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57065-181">Relative path of hello probe.</span></span> <span data-ttu-id="57065-182">ruta de acceso válida de Hola se inicia desde '/'.</span><span class="sxs-lookup"><span data-stu-id="57065-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="57065-183">sondeo de Hola se envía demasiado\<protocolo\>://\<host\>:\<puerto\>\<ruta de acceso\></span><span class="sxs-lookup"><span data-stu-id="57065-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="57065-184">Intervalo</span><span class="sxs-lookup"><span data-stu-id="57065-184">Interval</span></span> |<span data-ttu-id="57065-185">Intervalo de sondeo en segundos.</span><span class="sxs-lookup"><span data-stu-id="57065-185">Probe interval in seconds.</span></span> <span data-ttu-id="57065-186">Se trata de un intervalo de tiempo de hello entre dos sondeos consecutivos.</span><span class="sxs-lookup"><span data-stu-id="57065-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="57065-187">Tiempo de espera</span><span class="sxs-lookup"><span data-stu-id="57065-187">Time-out</span></span> |<span data-ttu-id="57065-188">Tiempo de espera del sondeo en segundos.</span><span class="sxs-lookup"><span data-stu-id="57065-188">Probe time-out in seconds.</span></span> <span data-ttu-id="57065-189">Si no se recibe una respuesta válida dentro de este período de tiempo de espera, el sondeo de Hola se marcará como incorrecta.</span><span class="sxs-lookup"><span data-stu-id="57065-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="57065-190">Umbral incorrecto</span><span class="sxs-lookup"><span data-stu-id="57065-190">Unhealthy threshold</span></span> |<span data-ttu-id="57065-191">Número de reintentos de sondeo.</span><span class="sxs-lookup"><span data-stu-id="57065-191">Probe retry count.</span></span> <span data-ttu-id="57065-192">servidor de back-end de Hola está marcado después de recuento de errores de sondeo consecutivos Hola alcanza el umbral de estado incorrecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="57065-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="57065-193">Solución</span><span class="sxs-lookup"><span data-stu-id="57065-193">Solution</span></span>

<span data-ttu-id="57065-194">Validar ese Hola que sondeo de estado personalizado está configurado correctamente como Hola tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="57065-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="57065-195">Además toohello anterior pasos, asegúrese también de siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="57065-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="57065-196">Asegúrese de que sondeo Hola se ha especificado correctamente según hello [guía](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="57065-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="57065-197">Si la puerta de enlace de aplicaciones está configurada para un único sitio, por hello predeterminado Host nombre debe especificarse como "127.0.0.1", a menos que en caso contrario, se configura en sondeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="57065-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="57065-198">Asegúrese de que una llamada toohttp: / /\<host\>:\<puerto\>\<ruta de acceso\> devuelve un código de resultado HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="57065-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="57065-199">Asegúrese de intervalo de tiempo de espera y UnhealtyThreshold dentro de los intervalos de hello aceptable.</span><span class="sxs-lookup"><span data-stu-id="57065-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="57065-200">Si el sondeo de uso de HTTPS, asegúrese de que ese servidor de back-end de hello no requiere SNI mediante la configuración de un certificado fallback en el propio servidor de back-end Hola.</span><span class="sxs-lookup"><span data-stu-id="57065-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="57065-201">Asegúrese de que intervalo y tiempo de espera, UnhealtyThreshold dentro de los intervalos de hello aceptable.</span><span class="sxs-lookup"><span data-stu-id="57065-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="57065-202">Tiempo de solicitud superado</span><span class="sxs-lookup"><span data-stu-id="57065-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="57065-203">Causa</span><span class="sxs-lookup"><span data-stu-id="57065-203">Cause</span></span>

<span data-ttu-id="57065-204">Cuando se recibe una solicitud de usuario, Application Gateway aplica Hola configurado reglas toohello solicitud y lo enruta la instancia de grupo de servidores de back-end de tooa.</span><span class="sxs-lookup"><span data-stu-id="57065-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="57065-205">Espera un intervalo de tiempo una respuesta de la instancia de back-end de hello configurable.</span><span class="sxs-lookup"><span data-stu-id="57065-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="57065-206">De forma predeterminada, este intervalo es de **30 segundos**.</span><span class="sxs-lookup"><span data-stu-id="57065-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="57065-207">Si la instancia de Application Gateway no recibe una respuesta de una aplicación back-end en este intervalo, la solicitud de usuario generaría un error 502.</span><span class="sxs-lookup"><span data-stu-id="57065-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="57065-208">Solución</span><span class="sxs-lookup"><span data-stu-id="57065-208">Solution</span></span>

<span data-ttu-id="57065-209">Puerta de enlace de aplicaciones permite a usuarios tooconfigure esta configuración a través de BackendHttpSetting, que puede ser, a continuación, aplica toodifferent grupos.</span><span class="sxs-lookup"><span data-stu-id="57065-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="57065-210">Estos grupos back-end pueden tener distintos elementos BackendHttpSetting y, por tanto, diferentes valores configurados para el tiempo de solicitud superado.</span><span class="sxs-lookup"><span data-stu-id="57065-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="57065-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57065-211">Next steps</span></span>

<span data-ttu-id="57065-212">Si hello pasos anteriores no resuelven Hola problema, abra un [incidencia de soporte técnico](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="57065-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

