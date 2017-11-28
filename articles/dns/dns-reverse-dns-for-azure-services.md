---
title: aaaReverse DNS para servicios de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure invertir las búsquedas DNS para los servicios hospedados en Azure"
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="dc9ba-103">Configuración de DNS inversos para servicios hospedados en Azure</span><span class="sxs-lookup"><span data-stu-id="dc9ba-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="dc9ba-104">Este artículo explica cómo tooconfigure invertir las búsquedas DNS para los servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="dc9ba-105">Los servicios de Azure utilizan direcciones IP asignadas por Azure y propiedad de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="dc9ba-106">Estos registros DNS inversos (registros PTR) deben crearse en hello correspondiente propiedad de Microsoft inversas zonas de búsqueda DNS.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="dc9ba-107">Este artículo se explica cómo toodo esto.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-107">This article explains how toodo this.</span></span>

<span data-ttu-id="dc9ba-108">Este escenario no se debe confundir con capacidad de hello demasiado[hospedan zonas de búsqueda DNS inversas de Hola para los intervalos IP asignadas en DNS de Azure](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="dc9ba-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="dc9ba-109">En este caso, los intervalos de IP Hola representados por la zona de búsqueda inversa de hello deben asignarse tooyour organización, normalmente por su ISP.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="dc9ba-110">Antes de leer este artículo, debe estar familiarizado con [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc9ba-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="dc9ba-111">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dc9ba-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="dc9ba-112">En el modelo de implementación del Administrador de recursos de hello, recursos de proceso (por ejemplo, las máquinas virtuales, conjuntos de escalas de máquina virtual o clústeres de Service Fabric) se exponen a través de un recurso de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="dc9ba-113">Búsquedas inversas de DNS se configuran mediante la propiedad de 'ReverseFqdn' hello de hello PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="dc9ba-114">En el modelo de implementación de hello clásico, los recursos de proceso se exponen mediante servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="dc9ba-115">Búsquedas inversas de DNS se configuran mediante la propiedad de 'ReverseDnsFqdn' hello de hello servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="dc9ba-116">DNS inversa no se admite actualmente para hello servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="dc9ba-117">Validación de registros de DNS inversos</span><span class="sxs-lookup"><span data-stu-id="dc9ba-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="dc9ba-118">Otros fabricantes no debe ser capaz de toocreate registros de DNS inverso para sus dominios DNS de tooyour de asignación de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="dc9ba-119">tooprevent, Azure solo permite la creación de hello de un registro DNS inversa donde nombre de dominio especificado en el registro DNS inverso hello es Hola igual o se resuelve como Hola nombre DNS o dirección IP de un PublicIpAddress o una nube de servicio en hello mismo suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="dc9ba-120">Solo se realiza la validación cuando el registro DNS inversa hello es establecer o modificar.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="dc9ba-121">No se llevan a cabo revalidaciones periódicas.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="dc9ba-122">Por ejemplo: supongamos que hello PublicIpAddress recurso tiene contosoapp1.northus.cloudapp.azure.com de nombre DNS de hello y una dirección IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="dc9ba-123">Hola ReverseFqdn para hello que publicipaddress puede especificarse como:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="dc9ba-124">nombre DNS de Hola para hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="dc9ba-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="dc9ba-125">Hello de nombres DNS a una PublicIpAddress diferentes en hello misma suscripción, como contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="dc9ba-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="dc9ba-126">Un personal de nombres DNS, como app1.contoso.com, siempre y cuando este nombre es *primer* configurado como un CNAME toocontosoapp1.northus.cloudapp.azure.com o tooa PublicIpAddress diferentes en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="dc9ba-127">Un personal de nombres DNS, como app1.contoso.com, siempre y cuando este nombre es *primer* configurado como una dirección IP de un registro toohello 23.96.52.53 o dirección IP de toohello de una PublicIpAddress diferentes en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="dc9ba-128">Hello mismas restricciones aplican tooreverse DNS para servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="dc9ba-129">DNS inverso para recursos de PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="dc9ba-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="dc9ba-130">Esta sección proporciona instrucciones detalladas sobre cómo tooconfigure inversa DNS para recursos de PublicIpAddress de modelo de implementación del Administrador de recursos de Hola, mediante PowerShell de Azure, Azure CLI 1.0 o 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="dc9ba-131">Configuración de DNS inversa para recursos PublicIpAddress no se admite actualmente a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="dc9ba-132">Azure admite un DNS inverso en la actualidad solo para los recursos de PublicIpAddress de IPv4.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="dc9ba-133">No es compatible para IPv6.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="dc9ba-134">Agregar tooan inversa de DNS existente las publicipaddresses a las</span><span class="sxs-lookup"><span data-stu-id="dc9ba-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="dc9ba-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc9ba-135">PowerShell</span></span>

<span data-ttu-id="dc9ba-136">tooadd inversa DNS tooan existente PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="dc9ba-137">tooadd invertir tooan DNS existente PublicIpAddress que aún no tenga un nombre DNS, también debe especificar un nombre DNS:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="dc9ba-138">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-138">Azure CLI 1.0</span></span>

<span data-ttu-id="dc9ba-139">tooadd inversa DNS tooan existente PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="dc9ba-140">tooadd invertir tooan DNS existente PublicIpAddress que aún no tenga un nombre DNS, también debe especificar un nombre DNS:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="dc9ba-141">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-141">Azure CLI 2.0</span></span>

<span data-ttu-id="dc9ba-142">tooadd inversa DNS tooan existente PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="dc9ba-143">tooadd invertir tooan DNS existente PublicIpAddress que aún no tenga un nombre DNS, también debe especificar un nombre DNS:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="dc9ba-144">Creación de una dirección IP pública con un DNS inverso</span><span class="sxs-lookup"><span data-stu-id="dc9ba-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="dc9ba-145">toocreate un nuevo PublicIpAddress con hello invertir ya ha especificado la propiedad DNS:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="dc9ba-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc9ba-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="dc9ba-147">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="dc9ba-148">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="dc9ba-149">Visualización de DNS inverso para una PublicIpAddress existente</span><span class="sxs-lookup"><span data-stu-id="dc9ba-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="dc9ba-150">Hola tooview el valor configurado para una PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="dc9ba-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc9ba-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="dc9ba-152">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="dc9ba-153">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="dc9ba-154">Eliminación de DNS inversos de direcciones IP públicas existentes</span><span class="sxs-lookup"><span data-stu-id="dc9ba-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="dc9ba-155">tooremove una propiedad DNS inversa de una PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="dc9ba-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc9ba-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="dc9ba-157">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="dc9ba-158">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dc9ba-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="dc9ba-159">Configuración de DNS inverso para Cloud Services</span><span class="sxs-lookup"><span data-stu-id="dc9ba-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="dc9ba-160">Esta sección proporciona instrucciones detalladas sobre cómo tooconfigure invertir DNS para servicios en la nube en el modelo de implementación clásico hello, uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="dc9ba-161">No se admite la configuración de DNS inverso para servicios en la nube a través de hello portal de Azure, Azure CLI 1.0 o 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="dc9ba-162">Agregar servicios de nube de tooexisting DNS inversa</span><span class="sxs-lookup"><span data-stu-id="dc9ba-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="dc9ba-163">tooadd un tooan de registro de DNS inversa existente de servicio en la nube:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="dc9ba-164">Creación de un servicio en la nube con un DNS inverso</span><span class="sxs-lookup"><span data-stu-id="dc9ba-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="dc9ba-165">toocreate un nuevo servicio de nube con la propiedad Hola DNS inversa ya especificada:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="dc9ba-166">Visualización de DNS inverso para los servicios en la nube existentes</span><span class="sxs-lookup"><span data-stu-id="dc9ba-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="dc9ba-167">Hola tooview invertir la propiedad DNS para un servicio de nube existente:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="dc9ba-168">Eliminación de DNS inverso de los servicios en la nube existentes</span><span class="sxs-lookup"><span data-stu-id="dc9ba-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="dc9ba-169">tooremove una propiedad DNS inversa de un servicio de nube existente:</span><span class="sxs-lookup"><span data-stu-id="dc9ba-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="dc9ba-170">P+F</span><span class="sxs-lookup"><span data-stu-id="dc9ba-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="dc9ba-171">¿Cuánto cuestan los registros de DNS inversos?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="dc9ba-172">Son gratuitos.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-172">They're free!</span></span>  <span data-ttu-id="dc9ba-173">No existe ningún coste adicional para las consultas o los registros de DNS inversos.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="dc9ba-174">¿Hola mi inversa resolver registros DNS de internet?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="dc9ba-175">Sí.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-175">Yes.</span></span> <span data-ttu-id="dc9ba-176">Una vez establecida la propiedad DNS inversa hello para el servicio de Azure, Azure administra todas las delegaciones DNS de Hola y zonas DNS necesario tooensure que invertir el registro DNS se resuelve para todos los usuarios de Internet.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="dc9ba-177">¿Se crean registros de DNS inverso predeterminados para mis servicios de Azure?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="dc9ba-178">No.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-178">No.</span></span> <span data-ttu-id="dc9ba-179">El DNS inverso es una característica opcional.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="dc9ba-180">No tiene valor predeterminado se crean registros DNS inversos si elige no tooconfigure ellos.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="dc9ba-181">¿Qué es el formato de hello para el nombre de dominio completo de hello (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="dc9ba-182">Los FQDN se especifican en orden progresivo y deben terminar con un punto (por ejemplo, "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="dc9ba-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="dc9ba-183">¿Qué ocurre si la comprobación de validación Hola Hola inversa DNS he especificado se produce un error?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="dc9ba-184">Donde hello comprobación de validación de DNS inversa se produce un error, se produce un error de registro DNS inversa de hello operación tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="dc9ba-185">Valor DNS inversa Hola correcto según sea necesario y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="dc9ba-186">¿Puedo configurar DNS inverso para Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="dc9ba-187">No.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-187">No.</span></span> <span data-ttu-id="dc9ba-188">DNS inversa no se admite para hello servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="dc9ba-189">¿Puedo configurar varios registros de DNS inversos para mi servicio de Azure?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="dc9ba-190">No.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-190">No.</span></span> <span data-ttu-id="dc9ba-191">Azure admite un único registro de DNS inverso por cada servicio en la nube de Azure o PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="dc9ba-192">¿Puedo configurar DNS inverso para los recursos de PublicIpAddress de IPv6?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="dc9ba-193">No.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-193">No.</span></span> <span data-ttu-id="dc9ba-194">Azure admite un DNS inverso en la actualidad solo para los recursos de PublicIpAddress de IPv4 y Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="dc9ba-195">¿Se pueden enviar mensajes de correo electrónico tooexternal dominios desde Mis servicios de cálculo de Azure?</span><span class="sxs-lookup"><span data-stu-id="dc9ba-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="dc9ba-196">No.</span><span class="sxs-lookup"><span data-stu-id="dc9ba-196">No.</span></span> [<span data-ttu-id="dc9ba-197">Servicios de proceso de Azure no admite dominios que envían mensajes de correo electrónico tooexternal</span><span class="sxs-lookup"><span data-stu-id="dc9ba-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="dc9ba-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc9ba-198">Next steps</span></span>

<span data-ttu-id="dc9ba-199">Para más información sobre los registros de DNS inverso, consulte información sobre la [búsqueda de DNS inverso en Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="dc9ba-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="dc9ba-200">Obtenga información acerca de cómo demasiado[zona de búsqueda inversa de Hola de host para el intervalo IP asignada por el ISP en DNS de Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="dc9ba-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

