---
title: DNS inversos para servicios de Azure | Microsoft Docs
description: "Aprenda a configurar búsquedas inversas de DNS para servicios hospedados en Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="4e538-103">Configuración de DNS inversos para servicios hospedados en Azure</span><span class="sxs-lookup"><span data-stu-id="4e538-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="4e538-104">En este artículo se explica cómo configurar búsquedas inversas de DNS para servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="4e538-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="4e538-105">Los servicios de Azure utilizan direcciones IP asignadas por Azure y propiedad de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e538-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="4e538-106">Estos registros de DNS inversos (registros PTR) deben crearse en las correspondientes zonas de búsqueda inversa DNS propiedad de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e538-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="4e538-107">En este artículo se explica cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="4e538-107">This article explains how to do this.</span></span>

<span data-ttu-id="4e538-108">Este escenario no debe confundirse con la capacidad de [hospedar las zonas de búsqueda inversa DNS para los intervalos IP asignados en DNS de Azure](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="4e538-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="4e538-109">En este caso, los intervalos IP representados por la zona de búsqueda inversa deben asignarse a su organización, normalmente por su ISP.</span><span class="sxs-lookup"><span data-stu-id="4e538-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="4e538-110">Antes de leer este artículo, debe estar familiarizado con [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e538-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="4e538-111">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4e538-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="4e538-112">En el modelo de implementación de Resource Manager, los recursos de proceso (como máquinas virtuales, conjuntos de escalado de máquinas virtuales o clústeres de Service Fabric) se exponen a través de un recurso de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="4e538-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="4e538-113">Las búsquedas inversas de DNS se configuran mediante la propiedad 'ReverseFqdn' de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="4e538-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="4e538-114">En el modelo de implementación clásico, los recursos de proceso se exponen mediante Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="4e538-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="4e538-115">Las búsquedas inversas de DNS se configuran mediante la propiedad 'ReverseDnsFqdn' del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="4e538-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="4e538-116">Actualmente no se admite DNS inverso para Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4e538-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="4e538-117">Validación de registros de DNS inversos</span><span class="sxs-lookup"><span data-stu-id="4e538-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="4e538-118">Otros fabricantes quizá no puedan crear registros de DNS inversos para la asignación del servicio de Azure a los dominios de DNS.</span><span class="sxs-lookup"><span data-stu-id="4e538-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="4e538-119">Para evitar esto, Azure solo permite la creación de un registro de DNS inverso en el que el nombre de dominio especificado en el registro de DNS inverso sea igual o se resuelva en el nombre DNS o dirección IP de PublicIpAddress o un servicio en la nube en la misma suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e538-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="4e538-120">Solo se realiza esta validación cuando se establece o modifica el registro de DNS inverso.</span><span class="sxs-lookup"><span data-stu-id="4e538-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="4e538-121">No se llevan a cabo revalidaciones periódicas.</span><span class="sxs-lookup"><span data-stu-id="4e538-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="4e538-122">Por ejemplo: supongamos que el recurso PublicIpAddress tiene el nombre DNS contosoapp1.northus.cloudapp.azure.com y la dirección IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="4e538-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="4e538-123">ReverseFqdn para PublicIpAddress puede especificarse como:</span><span class="sxs-lookup"><span data-stu-id="4e538-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="4e538-124">El nombre DNS para PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="4e538-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="4e538-125">El nombre DNS para otra PublicIpAddress de la misma suscripción, como contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="4e538-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="4e538-126">Un nombre DNS personal, como app1.contoso.com, siempre y cuando este nombre esté configurado *primero* como CNAME en contosoapp1.northus.cloudapp.azure.com o en otra PublicIpAddress de la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="4e538-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="4e538-127">Un nombre DNS personal, como app1.contoso.com, siempre y cuando este nombre esté configurado *primero* como registro D en la dirección IP 23.96.52.53 o en la dirección IP de otra PublicIpAddress de la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="4e538-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="4e538-128">Se aplican las mismas restricciones a DNS inverso para Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="4e538-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="4e538-129">DNS inverso para recursos de PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4e538-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="4e538-130">Esta sección proporciona instrucciones detalladas acerca de cómo configurar DNS inverso para recursos de PublicIpAddress en el modelo de implementación de Resource Manager, mediante Azure PowerShell, CLI de Azure 1.0 o CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="4e538-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="4e538-131">La configuración de DNS inverso para recursos de PublicIpAddress no está actualmente admitida a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4e538-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="4e538-132">Azure admite un DNS inverso en la actualidad solo para los recursos de PublicIpAddress de IPv4.</span><span class="sxs-lookup"><span data-stu-id="4e538-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="4e538-133">No es compatible para IPv6.</span><span class="sxs-lookup"><span data-stu-id="4e538-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="4e538-134">Incorporación de DNS inversos a PublicIpAddresses existentes</span><span class="sxs-lookup"><span data-stu-id="4e538-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="4e538-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e538-135">PowerShell</span></span>

<span data-ttu-id="4e538-136">Para agregar un DNS inverso a una PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="4e538-137">Para agregar un DNS inverso a una PublicIpAddress existente que no tenga aún un nombre DNS, debe especificar también un nombre DNS:</span><span class="sxs-lookup"><span data-stu-id="4e538-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="4e538-138">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4e538-138">Azure CLI 1.0</span></span>

<span data-ttu-id="4e538-139">Para agregar un DNS inverso a una PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="4e538-140">Para agregar un DNS inverso a una PublicIpAddress existente que no tenga aún un nombre DNS, debe especificar también un nombre DNS:</span><span class="sxs-lookup"><span data-stu-id="4e538-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="4e538-141">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4e538-141">Azure CLI 2.0</span></span>

<span data-ttu-id="4e538-142">Para agregar un DNS inverso a una PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="4e538-143">Para agregar un DNS inverso a una PublicIpAddress existente que no tenga aún un nombre DNS, debe especificar también un nombre DNS:</span><span class="sxs-lookup"><span data-stu-id="4e538-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="4e538-144">Creación de una dirección IP pública con un DNS inverso</span><span class="sxs-lookup"><span data-stu-id="4e538-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="4e538-145">Para crear una nueva PublicIpAddress con la propiedad de DNS inverso ya especificada:</span><span class="sxs-lookup"><span data-stu-id="4e538-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="4e538-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e538-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="4e538-147">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4e538-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="4e538-148">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4e538-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="4e538-149">Visualización de DNS inverso para una PublicIpAddress existente</span><span class="sxs-lookup"><span data-stu-id="4e538-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="4e538-150">Para ver el valor configurado para una PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="4e538-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e538-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="4e538-152">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4e538-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="4e538-153">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4e538-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="4e538-154">Eliminación de DNS inversos de direcciones IP públicas existentes</span><span class="sxs-lookup"><span data-stu-id="4e538-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="4e538-155">Para quitar una propiedad de DNS inverso de una PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="4e538-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e538-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="4e538-157">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4e538-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="4e538-158">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4e538-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="4e538-159">Configuración de DNS inverso para Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4e538-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="4e538-160">Esta sección proporciona instrucciones detalladas sobre cómo configurar DNS inverso para Cloud Services en el modelo de implementación clásico, mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e538-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="4e538-161">No se admite la configuración de DNS inverso para Cloud Services a través de Azure Portal, CLI de Azure 1.0 o CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="4e538-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="4e538-162">Adición de DNS inverso a los servicios en la nube existentes</span><span class="sxs-lookup"><span data-stu-id="4e538-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="4e538-163">Para agregar un registro DNS inverso a un servicio en la nube existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="4e538-164">Creación de un servicio en la nube con un DNS inverso</span><span class="sxs-lookup"><span data-stu-id="4e538-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="4e538-165">Para crear un nuevo servicio en la nube con la propiedad de DNS inverso ya especificada:</span><span class="sxs-lookup"><span data-stu-id="4e538-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="4e538-166">Visualización de DNS inverso para los servicios en la nube existentes</span><span class="sxs-lookup"><span data-stu-id="4e538-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="4e538-167">Para ver la propiedad de DNS inverso de un servicio en la nube existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="4e538-168">Eliminación de DNS inverso de los servicios en la nube existentes</span><span class="sxs-lookup"><span data-stu-id="4e538-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="4e538-169">Para quitar un propiedad de DNS inverso de un servicio en la nube existente:</span><span class="sxs-lookup"><span data-stu-id="4e538-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="4e538-170">P+F</span><span class="sxs-lookup"><span data-stu-id="4e538-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="4e538-171">¿Cuánto cuestan los registros de DNS inversos?</span><span class="sxs-lookup"><span data-stu-id="4e538-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="4e538-172">Son gratuitos.</span><span class="sxs-lookup"><span data-stu-id="4e538-172">They're free!</span></span>  <span data-ttu-id="4e538-173">No existe ningún coste adicional para las consultas o los registros de DNS inversos.</span><span class="sxs-lookup"><span data-stu-id="4e538-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="4e538-174">¿Se resolverán mis registros de DNS inversos desde Internet?</span><span class="sxs-lookup"><span data-stu-id="4e538-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="4e538-175">Sí.</span><span class="sxs-lookup"><span data-stu-id="4e538-175">Yes.</span></span> <span data-ttu-id="4e538-176">Cuando haya configurado la propiedad de DNS inverso para el servicio de Azure, Azure administrará todas las delegaciones y zonas DNS necesarias para garantizar que el registro de DNS inverso se resuelve para todos los usuarios de Internet.</span><span class="sxs-lookup"><span data-stu-id="4e538-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="4e538-177">¿Se crean registros de DNS inverso predeterminados para mis servicios de Azure?</span><span class="sxs-lookup"><span data-stu-id="4e538-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="4e538-178">No.</span><span class="sxs-lookup"><span data-stu-id="4e538-178">No.</span></span> <span data-ttu-id="4e538-179">El DNS inverso es una característica opcional.</span><span class="sxs-lookup"><span data-stu-id="4e538-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="4e538-180">Si decide no configurarla, no se crea ningún registro de DNS inverso predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4e538-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="4e538-181">¿Cuál es el formato del nombre de dominio completo (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="4e538-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="4e538-182">Los FQDN se especifican en orden progresivo y deben terminar con un punto (por ejemplo, "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="4e538-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="4e538-183">¿Qué ocurre si no se supera la comprobación de validación para el DNS inverso que he especificado?</span><span class="sxs-lookup"><span data-stu-id="4e538-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="4e538-184">Cuando se produce un error en la comprobación de validación de DNS inverso, se produce un error en la operación para configurar el registro de DNS inverso.</span><span class="sxs-lookup"><span data-stu-id="4e538-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="4e538-185">Corrija el valor de DNS inverso según sea necesario y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="4e538-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="4e538-186">¿Puedo configurar DNS inverso para Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="4e538-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="4e538-187">No.</span><span class="sxs-lookup"><span data-stu-id="4e538-187">No.</span></span> <span data-ttu-id="4e538-188">No se admite DNS inverso para Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4e538-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="4e538-189">¿Puedo configurar varios registros de DNS inversos para mi servicio de Azure?</span><span class="sxs-lookup"><span data-stu-id="4e538-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="4e538-190">No.</span><span class="sxs-lookup"><span data-stu-id="4e538-190">No.</span></span> <span data-ttu-id="4e538-191">Azure admite un único registro de DNS inverso por cada servicio en la nube de Azure o PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="4e538-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="4e538-192">¿Puedo configurar DNS inverso para los recursos de PublicIpAddress de IPv6?</span><span class="sxs-lookup"><span data-stu-id="4e538-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="4e538-193">No.</span><span class="sxs-lookup"><span data-stu-id="4e538-193">No.</span></span> <span data-ttu-id="4e538-194">Azure admite un DNS inverso en la actualidad solo para los recursos de PublicIpAddress de IPv4 y Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="4e538-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="4e538-195">¿Puedo enviar correos electrónicos a dominios externos desde mis servicios de proceso de Azure?</span><span class="sxs-lookup"><span data-stu-id="4e538-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="4e538-196">No.</span><span class="sxs-lookup"><span data-stu-id="4e538-196">No.</span></span> <span data-ttu-id="4e538-197">[Los servicios de proceso de Azure no admiten el envío de correos electrónicos a dominios externos](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/).</span><span class="sxs-lookup"><span data-stu-id="4e538-197">[Azure Compute services do not support sending emails to external domains](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e538-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e538-198">Next steps</span></span>

<span data-ttu-id="4e538-199">Para más información sobre los registros de DNS inverso, consulte información sobre la [búsqueda de DNS inverso en Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="4e538-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="4e538-200">Aprenda cómo [hospedar la zona de búsqueda inversa para el intervalo IP asignado por el ISP en DNS de Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="4e538-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

