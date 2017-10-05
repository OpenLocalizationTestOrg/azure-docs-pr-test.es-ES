---
title: "Alojamiento de zonas de búsqueda inversa DNS en DNS de Azure | Microsoft Docs"
description: "Aprenda a usar DNS de Azure para hospedar las zonas de búsqueda inversa de DNS para los intervalos IP"
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
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="b815d-103">Alojamiento de zonas de búsqueda inversa DNS en DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="b815d-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="b815d-104">Este artículo explica cómo hospedar las zonas de búsqueda inversa DNS para los intervalos IP asignados en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b815d-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="b815d-105">Los intervalos IP representados por la zona de búsqueda inversa deben asignarse a su organización, normalmente por su ISP.</span><span class="sxs-lookup"><span data-stu-id="b815d-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="b815d-106">Para configurar DNS inverso para la dirección IP propiedad de Azure asignada a su servicio de Azure, consulte cómo [configurar la búsqueda inversa de las direcciones IP asignadas a su servicio Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="b815d-107">Antes de leer este artículo, debe estar familiarizado con [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="b815d-108">Este artículo le guiará por los pasos necesarios para crear su primera zona de búsqueda inversa DNS y su primer registro de DNS con Azure Portal, Azure PowerShell, CLI de Azure 1.0 o CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="b815d-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="b815d-109">Creación de una zona de búsqueda inversa DNS</span><span class="sxs-lookup"><span data-stu-id="b815d-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="b815d-110">Inicie sesión en el [Portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b815d-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="b815d-111">En el menú Concentrador, haga clic en **Nuevo** > **Redes** > y, luego, en **Zona DNS** para abrir la hoja **Crear zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="b815d-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="b815d-113">En la hoja **Crear zona DNS**, asígnele un nombre a la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b815d-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="b815d-114">El nombre de la zona está diseñado de forma diferente para los prefijos IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="b815d-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="b815d-115">Use cualquiera de la instrucciones para [IPV4](#ipv4) o [IPv6](#ipv6) a fin de asignar un nombre a la zona.</span><span class="sxs-lookup"><span data-stu-id="b815d-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="b815d-116">Cuando haya terminado, haga clic en **Crear** para crear la zona.</span><span class="sxs-lookup"><span data-stu-id="b815d-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="b815d-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="b815d-117">IPv4</span></span>

<span data-ttu-id="b815d-118">El nombre de una zona de búsqueda inversa IPv4 se basa en el intervalo IP que representa.</span><span class="sxs-lookup"><span data-stu-id="b815d-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="b815d-119">Tendrá el siguiente formato: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="b815d-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="b815d-120">Para ver ejemplos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="b815d-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="b815d-121">Al crear zonas de búsqueda inversa de DNS sin clases en DNS de Azure, debe usar un guion (`-`) en lugar de una barra diagonal ('/ ') en el nombre de la zona.</span><span class="sxs-lookup"><span data-stu-id="b815d-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="b815d-122">Por ejemplo, para el intervalo IP 192.0.2.128/26, debe utilizar `128-26.2.0.192.in-addr.arpa` como nombre de zona en lugar de `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="b815d-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="b815d-123">Esto se debe a que, aunque ambos sean compatibles con los estándares DNS, los nombres de zona DNS que contienen el carácter de barra diagonal (`/`) no se admiten en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b815d-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="b815d-124">En el ejemplo siguiente se muestra cómo crear una zona DNS inversa de 'Clase C' denominada `2.0.192.in-addr.arpa` en DNS de Azure mediante Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="b815d-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Creación de una zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="b815d-126">'Ubicación del grupo de recursos' define la ubicación para el grupo de recursos y no tiene efecto alguno sobre la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b815d-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="b815d-127">La ubicación de la zona DNS siempre es 'global' y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="b815d-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="b815d-128">Los ejemplos siguientes muestran cómo realizar esta tarea con Azure PowerShell y la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b815d-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b815d-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b815d-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="b815d-130">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b815d-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="b815d-131">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b815d-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="b815d-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="b815d-132">IPv6</span></span>

<span data-ttu-id="b815d-133">El nombre de una zona de búsqueda inversa IPv6 debe tener el formato siguiente: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="b815d-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="b815d-134">Para ver ejemplos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="b815d-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="b815d-135">En el ejemplo siguiente se muestra cómo crear una zona de búsqueda inversa DNS IPv6 denominada `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` en DNS de Azure mediante Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="b815d-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Creación de una zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="b815d-137">'Ubicación del grupo de recursos' define la ubicación para el grupo de recursos y no tiene efecto alguno sobre la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b815d-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="b815d-138">La ubicación de la zona DNS siempre es 'global' y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="b815d-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="b815d-139">Los ejemplos siguientes muestran cómo realizar esta tarea con Azure PowerShell y la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b815d-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b815d-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b815d-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="b815d-141">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b815d-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="b815d-142">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b815d-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="b815d-143">Delegación de una zona de búsqueda inversa DNS</span><span class="sxs-lookup"><span data-stu-id="b815d-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="b815d-144">Al haber creado la zona de búsqueda inversa DNS, debe asegurarse de que la zona se delega desde la zona primaria.</span><span class="sxs-lookup"><span data-stu-id="b815d-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="b815d-145">La delegación de DNS permite que el proceso de resolución de nombres DNS encuentre los servidores de nombres que hospedan la zona de búsqueda inversa DNS.</span><span class="sxs-lookup"><span data-stu-id="b815d-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="b815d-146">Esto permite a los servidores de nombres responder a consultas DNS inversas para las direcciones IP en el intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="b815d-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="b815d-147">Para las zonas de búsqueda directa, el proceso de delegación de una zona DNS se describe en [Delegación de un dominio en DNS de Azure](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="b815d-148">La delegación de zonas de búsqueda inversa funciona del mismo modo.</span><span class="sxs-lookup"><span data-stu-id="b815d-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="b815d-149">La única diferencia es que debe configurar los servidores de nombres con el ISP que ha proporcionado el intervalo IP, en lugar de su registrador de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="b815d-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="b815d-150">Creación de un registro PTR DNS</span><span class="sxs-lookup"><span data-stu-id="b815d-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="b815d-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="b815d-151">IPv4</span></span>

<span data-ttu-id="b815d-152">En el ejemplo siguiente, se le guiará a través del proceso de creación de un registro PTR en una zona DNS inversa mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b815d-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="b815d-153">Para crear otros tipos de registros y modificar los que ya existan, consulte [Administración de registros y conjuntos de registros DNS mediante Azure Portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="b815d-154">En la parte superior de la hoja **Zona DNS**, seleccione **+ Conjunto de registros** para abrir la hoja **Agregar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="b815d-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="b815d-156">En la hoja **Agregar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="b815d-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="b815d-157">Seleccione **PTR** en el menú "**Tipo**" de registro.</span><span class="sxs-lookup"><span data-stu-id="b815d-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="b815d-158">El nombre del conjunto de registros para un registro PTR debe ser el resto de la dirección IPv4 en orden inverso.</span><span class="sxs-lookup"><span data-stu-id="b815d-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="b815d-159">En este ejemplo, los tres primeros octetos ya están rellenados como parte del nombre de la zona (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="b815d-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="b815d-160">Por lo tanto, solo se proporciona el último octeto en el campo de nombre.</span><span class="sxs-lookup"><span data-stu-id="b815d-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="b815d-161">Por ejemplo, podría denominar el conjunto de registros "**15**" para un recurso cuya dirección IP es 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="b815d-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="b815d-162">En el campo "**Nombre de dominio**", escriba el nombre de dominio completo (FQDN) del recurso mediante la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="b815d-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="b815d-163">Haga clic en **Aceptar** en la parte inferior de la hoja para crear el registro DNS.</span><span class="sxs-lookup"><span data-stu-id="b815d-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![Agregar conjunto de registros](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="b815d-165">Los ejemplos siguientes muestran cómo realizar esta tarea con PowerShell y la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b815d-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b815d-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b815d-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="b815d-167">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b815d-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="b815d-168">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b815d-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="b815d-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="b815d-169">IPv6</span></span>

<span data-ttu-id="b815d-170">En el ejemplo siguiente, se le guiará a través del proceso de creación de un registro 'PTR'.</span><span class="sxs-lookup"><span data-stu-id="b815d-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="b815d-171">Para crear otros tipos de registros y modificar los que ya existan, consulte [Administración de registros y conjuntos de registros DNS mediante Azure Portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="b815d-172">En la parte superior de la hoja **Zona DNS**, seleccione **+ Conjunto de registros** para abrir la hoja **Agregar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="b815d-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="b815d-174">En la hoja **Agregar conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="b815d-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="b815d-175">Seleccione **PTR** en el menú "**Tipo**" de registro.</span><span class="sxs-lookup"><span data-stu-id="b815d-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="b815d-176">El nombre del conjunto de registros para un registro PTR debe ser el resto de la dirección IPv6 en orden inverso.</span><span class="sxs-lookup"><span data-stu-id="b815d-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="b815d-177">No puede contener ninguna compresión de ceros.</span><span class="sxs-lookup"><span data-stu-id="b815d-177">It must not include any zero compression.</span></span> <span data-ttu-id="b815d-178">En este ejemplo, los primeros 64 bits de IPv6 se rellenan como parte del nombre de zona (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="b815d-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="b815d-179">Por lo tanto, solo se proporcionan los últimos 64 bits en el campo de nombre.</span><span class="sxs-lookup"><span data-stu-id="b815d-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="b815d-180">Los últimos 64 bits de la dirección IP se escriben en orden inverso, con un punto como delimitador entre cada número hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="b815d-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="b815d-181">Por ejemplo, podría denominar el conjunto de registros "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para un recurso cuya dirección IP es 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="b815d-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="b815d-182">En el campo "**Nombre de dominio**", escriba el nombre de dominio completo (FQDN) del recurso mediante la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="b815d-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="b815d-183">Haga clic en **Aceptar** en la parte inferior de la hoja para crear el registro DNS.</span><span class="sxs-lookup"><span data-stu-id="b815d-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![Hoja Agregar conjunto de registros](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="b815d-185">Los ejemplos siguientes muestran cómo realizar esta tarea con PowerShell y la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b815d-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b815d-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b815d-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="b815d-187">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b815d-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="b815d-188">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b815d-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="b815d-189">Visualización de los registros</span><span class="sxs-lookup"><span data-stu-id="b815d-189">View Records</span></span>

<span data-ttu-id="b815d-190">Para ver los registros que ha creado, vaya a la zona DNS en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b815d-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="b815d-191">En la parte inferior de la hoja **Zona DNS**, puede consultar los registros correspondientes a la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b815d-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="b815d-192">Debería ver los registros SOA y NS predeterminados, que se crean en cada zona, además de todos los nuevos que haya creado.</span><span class="sxs-lookup"><span data-stu-id="b815d-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="b815d-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="b815d-193">IPv4</span></span>

<span data-ttu-id="b815d-194">Hoja de zona DNS, que muestra los registros PTR de IPv4:</span><span class="sxs-lookup"><span data-stu-id="b815d-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="b815d-196">Los ejemplos siguientes muestran cómo ver los registros PTR con PowerShell o la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b815d-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b815d-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b815d-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="b815d-198">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b815d-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="b815d-199">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b815d-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="b815d-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="b815d-200">IPv6</span></span>

<span data-ttu-id="b815d-201">Hoja de zona DNS, que muestra los registros PTR de IPv6:</span><span class="sxs-lookup"><span data-stu-id="b815d-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="b815d-203">Los ejemplos siguientes muestran cómo ver los registros con PowerShell o la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b815d-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b815d-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b815d-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="b815d-205">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b815d-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="b815d-206">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b815d-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="b815d-207">P+F</span><span class="sxs-lookup"><span data-stu-id="b815d-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="b815d-208">¿Puedo hospedar zonas de búsqueda inversa DNS para mis bloques IP asignados por el ISP en DNS de Azure?</span><span class="sxs-lookup"><span data-stu-id="b815d-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="b815d-209">Sí.</span><span class="sxs-lookup"><span data-stu-id="b815d-209">Yes.</span></span> <span data-ttu-id="b815d-210">El hospedaje de zonas de búsqueda inversa (ARPA) para sus propios intervalos de IP en DNS de Azure está totalmente permitido.</span><span class="sxs-lookup"><span data-stu-id="b815d-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="b815d-211">Cree la zona de búsqueda inversa en DNS de Azure tal como se explica en este artículo y trabaje con su ISP para [delegar la zona](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="b815d-212">Después puede administrar los registros PTR de cada búsqueda inversa igual que otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="b815d-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="b815d-213">¿Cuánto cuesta el hospedaje de mi zona de búsqueda inversa DNS?</span><span class="sxs-lookup"><span data-stu-id="b815d-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="b815d-214">El hospedaje de una zona de búsqueda inversa DNS para su bloque de direcciones IP asignadas por el ISP en DNS de Azure se cobra según las [tarifas estándar de DNS de Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="b815d-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="b815d-215">Puedo hospedar zonas de búsqueda inversa DNS para direcciones IPv4 e IPv6 en DNS de Azure?</span><span class="sxs-lookup"><span data-stu-id="b815d-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="b815d-216">Sí.</span><span class="sxs-lookup"><span data-stu-id="b815d-216">Yes.</span></span> <span data-ttu-id="b815d-217">En este artículo se explica cómo crear zonas de búsqueda inversa DNS de IPv4 e IPv6 en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b815d-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="b815d-218">¿Puedo importar una zona de búsqueda inversa DNS existente?</span><span class="sxs-lookup"><span data-stu-id="b815d-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="b815d-219">Sí.</span><span class="sxs-lookup"><span data-stu-id="b815d-219">Yes.</span></span> <span data-ttu-id="b815d-220">Puede utilizar la CLI de Azure para importar las zonas DNS existentes a DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b815d-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="b815d-221">Esto funciona para las zonas de búsqueda directa y las zonas de búsqueda inversa.</span><span class="sxs-lookup"><span data-stu-id="b815d-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="b815d-222">Para más información, consulte [Importación y exportación de un archivo de zona DNS mediante la CLI de Azure](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b815d-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b815d-223">Next steps</span></span>

<span data-ttu-id="b815d-224">Para más información sobre los registros de DNS inverso, consulte información sobre la [búsqueda de DNS inverso en Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="b815d-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="b815d-225">Aprenda a [administrar registros de DNS inversos para servicios de Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="b815d-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
