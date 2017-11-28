---
title: "aaaHosting invertir zonas de búsqueda DNS en el DNS de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola de toouse DNS de Azure toohost invertir zonas de búsqueda DNS para los intervalos de IP"
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="d77e7-103">Alojamiento de zonas de búsqueda inversa DNS en DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="d77e7-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="d77e7-104">Este artículo explica cómo toohost Hola invertir zonas de búsqueda DNS para los intervalos IP asignadas en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d77e7-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="d77e7-105">intervalos IP de Hello representados por la zona de búsqueda inversa de hello deben asignarse tooyour organización, normalmente por su ISP.</span><span class="sxs-lookup"><span data-stu-id="d77e7-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="d77e7-106">tooconfigure inversa de DNS para la propiedad de Azure IP dirección asignada tooyour servicio de Azure, consulte [configurar la búsqueda inversa de Hola para direcciones IP que Hola asignan tooyour servicio de Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="d77e7-107">Antes de leer este artículo, debe estar familiarizado con [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="d77e7-108">Este artículo le guiará a través de hello pasos toocreate la primera zona de búsqueda inversa DNS y el registro mediante Hola portal de Azure, PowerShell de Azure, Azure CLI 1.0 o 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d77e7-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="d77e7-109">Creación de una zona de búsqueda inversa DNS</span><span class="sxs-lookup"><span data-stu-id="d77e7-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="d77e7-110">Inicie sesión en toohello [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d77e7-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="d77e7-111">En el menú del concentrador hello, haga clic en y haga clic en **New** > **red** > y, a continuación, haga clic en **zona DNS** tooopen hello **zona de DNS crear**hoja.</span><span class="sxs-lookup"><span data-stu-id="d77e7-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="d77e7-113">En hello **zona DNS crear** hoja, el nombre de la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="d77e7-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="d77e7-114">nombre Hola de zona de Hola está diseñada de forma diferente para los prefijos de IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="d77e7-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="d77e7-115">Usar cualquier instrucciones Hola de [IPV4](#ipv4) o [IPv6](#ipv6) tooname su zona.</span><span class="sxs-lookup"><span data-stu-id="d77e7-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="d77e7-116">Cuando haya terminado haga clic en **crear** zona de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d77e7-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d77e7-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="d77e7-117">IPv4</span></span>

<span data-ttu-id="d77e7-118">nombre de Hola de una zona de búsqueda inversa IPv4 se basa en el intervalo IP de hello representa.</span><span class="sxs-lookup"><span data-stu-id="d77e7-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="d77e7-119">Debería ser Hola siguiendo el formato: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="d77e7-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="d77e7-120">Para ver ejemplos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="d77e7-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="d77e7-121">Al crear interdominios sin clases zonas de búsqueda inversas de DNS en DNS de Azure, debe usar un guión (`-`) en lugar de una barra diagonal ('/ ') en nombre de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="d77e7-122">Por ejemplo, para hello IP intervalo 192.0.2.128/26, debe utilizar `128-26.2.0.192.in-addr.arpa` como nombre de la zona de hello en lugar de `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="d77e7-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="d77e7-123">Esto es porque, aunque ambos son compatibles con los estándares de DNS hello, nombres que contengan diagonal Hola la zona DNS (`/`) caracteres no se admiten en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d77e7-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="d77e7-124">Hello en el ejemplo siguiente se muestra cómo toocreate 'Clase C' invertir la zona DNS con el nombre `2.0.192.in-addr.arpa` en DNS de Azure a través de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="d77e7-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Creación de una zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="d77e7-126">Hola 'Ubicación del grupo de recursos' define la ubicación de hello para el grupo de recursos de hello y no tiene ningún efecto en la zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="d77e7-127">ubicación de la zona DNS Hola siempre es 'global' y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="d77e7-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d77e7-128">Hello en los ejemplos siguientes muestran cómo toocomplete esta tarea con hello CLI de Azure y Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d77e7-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d77e7-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d77e7-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d77e7-130">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d77e7-131">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d77e7-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="d77e7-132">IPv6</span></span>

<span data-ttu-id="d77e7-133">Hola nombre de una zona de búsqueda inversa IPv6 debe ser Hola siguiendo el formato: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="d77e7-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="d77e7-134">Para ver ejemplos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="d77e7-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="d77e7-135">Hello en el ejemplo siguiente se muestra cómo toocreate una zona de búsqueda DNS inversa IPv6 denominado `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` en DNS de Azure a través de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="d77e7-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Creación de una zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="d77e7-137">Hola 'Ubicación del grupo de recursos' define la ubicación de hello para el grupo de recursos de hello y no tiene ningún efecto en la zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="d77e7-138">ubicación de la zona DNS Hola siempre es 'global' y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="d77e7-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d77e7-139">Hello en los ejemplos siguientes muestran cómo toocomplete esta tarea con hello CLI de Azure y Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d77e7-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d77e7-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d77e7-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="d77e7-141">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="d77e7-142">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="d77e7-143">Delegación de una zona de búsqueda inversa DNS</span><span class="sxs-lookup"><span data-stu-id="d77e7-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="d77e7-144">Al haber creado la zona de búsqueda inversa de DNS, debe asegurarse de que esa zona Hola se delega de la zona primaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="d77e7-145">Delegación de DNS permite a Hola resolución proceso toofind Hola nombre servidores de nombres DNS hospeda la zona de búsqueda inversa de DNS.</span><span class="sxs-lookup"><span data-stu-id="d77e7-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="d77e7-146">Esto permite que los servidores tooanswer DNS inversas consultas de nombres para las direcciones IP de hello en el intervalo de direcciones.</span><span class="sxs-lookup"><span data-stu-id="d77e7-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="d77e7-147">Para las zonas de búsqueda directa, el proceso de Hola de delegación de una zona DNS se describe en [delegar su tooAzure de dominio DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="d77e7-148">La delegación de zonas de búsqueda inversa funciona Hola igual.</span><span class="sxs-lookup"><span data-stu-id="d77e7-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="d77e7-149">Hola única diferencia es que necesita servidores de nombres de hello tooconfigure con hello ISP que proporciona el intervalo de IP, en lugar de su registrador de nombres de dominio.</span><span class="sxs-lookup"><span data-stu-id="d77e7-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="d77e7-150">Creación de un registro PTR DNS</span><span class="sxs-lookup"><span data-stu-id="d77e7-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="d77e7-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="d77e7-151">IPv4</span></span>

<span data-ttu-id="d77e7-152">Hello en el ejemplo siguiente se le guía a través del proceso de Hola de creación de un registro PTR en una zona DNS inversa de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d77e7-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="d77e7-153">Para otros tipos de registro y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros mediante el uso de Hola portal de Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="d77e7-154">En parte superior de Hola de hello **zona DNS** hoja, seleccione **+ grabar conjunto** tooopen hello **Agregar conjunto de registros** hoja.</span><span class="sxs-lookup"><span data-stu-id="d77e7-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="d77e7-156">En hello **Agregar conjunto de registros** hoja.</span><span class="sxs-lookup"><span data-stu-id="d77e7-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="d77e7-157">Seleccione **PTR** de registro de hello "**tipo**" menú.</span><span class="sxs-lookup"><span data-stu-id="d77e7-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="d77e7-158">Hello nombre del conjunto de registros de Hola para un registro PTR debe rest de hello toobe de hello dirección IPv4 en orden inverso.</span><span class="sxs-lookup"><span data-stu-id="d77e7-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="d77e7-159">En este ejemplo, hello tres primeros octetos ya se han rellenado como parte del nombre de la zona de hello (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="d77e7-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="d77e7-160">Por lo tanto, solo Hola último octeto se proporciona en el campo de nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="d77e7-161">Por ejemplo, podría denominar el conjunto de registros "**15**" para un recurso cuya dirección IP es 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="d77e7-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="d77e7-162">Hola "**nombre de dominio**", escriba el nombre de dominio completo de hello (FQDN) del recurso de hello con IP Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="d77e7-163">Seleccione **Aceptar** final Hola Hola hoja toocreate Hola de registro de DNS.</span><span class="sxs-lookup"><span data-stu-id="d77e7-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![Agregar conjunto de registros](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="d77e7-165">Hello éstos son algunos ejemplos sobre cómo toocomplete esta tarea con hello AzureCLI y PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d77e7-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d77e7-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d77e7-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="d77e7-167">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="d77e7-168">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="d77e7-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="d77e7-169">IPv6</span></span>

<span data-ttu-id="d77e7-170">Hola siguiente ejemplo explica Hola proceso de creación de nuevo registro de 'PTR'.</span><span class="sxs-lookup"><span data-stu-id="d77e7-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="d77e7-171">Para otros tipos de registro y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros mediante el uso de Hola portal de Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="d77e7-172">En parte superior de Hola de hello **hoja de zona DNS**, seleccione **+ grabar conjunto** tooopen Hola **Agregar conjunto de registros** hoja.</span><span class="sxs-lookup"><span data-stu-id="d77e7-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="d77e7-174">En hello **Agregar conjunto de registros** hoja.</span><span class="sxs-lookup"><span data-stu-id="d77e7-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="d77e7-175">Seleccione **PTR** de registro de hello "**tipo**" menú.</span><span class="sxs-lookup"><span data-stu-id="d77e7-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="d77e7-176">Hello nombre del conjunto de registros de Hola para un registro PTR debe rest de hello toobe de hello dirección IPv6 en orden inverso.</span><span class="sxs-lookup"><span data-stu-id="d77e7-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="d77e7-177">No puede contener ninguna compresión de ceros.</span><span class="sxs-lookup"><span data-stu-id="d77e7-177">It must not include any zero compression.</span></span> <span data-ttu-id="d77e7-178">En este ejemplo, Hola primeros 64 bits de hello IPv6 se rellenan como parte del nombre de la zona de hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="d77e7-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="d77e7-179">Por lo tanto, se proporcionan solo Hola últimos 64 bits en el campo de nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="d77e7-180">Hola últimos 64 bits de la dirección IP de Hola se escriben en orden inverso, con un punto como delimitador de hello entre cada número hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="d77e7-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="d77e7-181">Por ejemplo, podría denominar el conjunto de registros "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para un recurso cuya dirección IP es 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="d77e7-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="d77e7-182">Hola "**nombre de dominio**", escriba el nombre de dominio completo de hello (FQDN) del recurso de hello con IP Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="d77e7-183">Seleccione **Aceptar** final Hola Hola hoja toocreate Hola de registro de DNS.</span><span class="sxs-lookup"><span data-stu-id="d77e7-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![Hoja Agregar conjunto de registros](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="d77e7-185">Hello éstos son algunos ejemplos sobre cómo toocomplete esta tarea con hello AzureCLI y PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d77e7-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d77e7-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d77e7-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="d77e7-187">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="d77e7-188">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="d77e7-189">Visualización de los registros</span><span class="sxs-lookup"><span data-stu-id="d77e7-189">View Records</span></span>

<span data-ttu-id="d77e7-190">registros de hello tooview ha creado, navegue tooyour zona DNS en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d77e7-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="d77e7-191">Hola reducir parte de hello **zona DNS** hoja, puede ver registros de Hola para zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="d77e7-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="d77e7-192">Debería ver Hola SOA y NS registros predeterminados, para que se crean en cada zona, además de todos los registros nuevos que haya creado.</span><span class="sxs-lookup"><span data-stu-id="d77e7-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d77e7-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="d77e7-193">IPv4</span></span>

<span data-ttu-id="d77e7-194">Hoja de zona DNS, que muestra los registros PTR de IPv4:</span><span class="sxs-lookup"><span data-stu-id="d77e7-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="d77e7-196">Hello en los ejemplos siguientes muestran cómo tooview Hola PTR registros mediante PowerShell u Hola CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="d77e7-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d77e7-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d77e7-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d77e7-198">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d77e7-199">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d77e7-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="d77e7-200">IPv6</span></span>

<span data-ttu-id="d77e7-201">Hoja de zona DNS, que muestra los registros PTR de IPv6:</span><span class="sxs-lookup"><span data-stu-id="d77e7-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Hoja de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="d77e7-203">siguiente Hola es ejemplos de cómo tooview Hola registros con hello AzureCLI y PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d77e7-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d77e7-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d77e7-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d77e7-205">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d77e7-206">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d77e7-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="d77e7-207">P+F</span><span class="sxs-lookup"><span data-stu-id="d77e7-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="d77e7-208">¿Puedo hospedar zonas de búsqueda inversa DNS para mis bloques IP asignados por el ISP en DNS de Azure?</span><span class="sxs-lookup"><span data-stu-id="d77e7-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="d77e7-209">Sí.</span><span class="sxs-lookup"><span data-stu-id="d77e7-209">Yes.</span></span> <span data-ttu-id="d77e7-210">Hospedan zonas de búsqueda inversa (ARPA) Hola para sus propios intervalos de IP en DNS de Azure es totalmente compatible.</span><span class="sxs-lookup"><span data-stu-id="d77e7-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="d77e7-211">Cree la zona de búsqueda inversa de hello en DNS de Azure como se explica en este artículo, a continuación, trabajar con su ISP demasiado[delegado Hola zona](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="d77e7-212">A continuación, puede administrar los registros PTR Hola para cada búsqueda inversa Hola mismo modo que otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="d77e7-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="d77e7-213">¿Cuánto cuesta el hospedaje de mi zona de búsqueda inversa DNS?</span><span class="sxs-lookup"><span data-stu-id="d77e7-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="d77e7-214">Hospedaje de zona de búsqueda DNS inversa hello para el bloque IP asignada por el ISP en DNS de Azure se aplican cargos en [tasas estándar de DNS de Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="d77e7-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="d77e7-215">Puedo hospedar zonas de búsqueda inversa DNS para direcciones IPv4 e IPv6 en DNS de Azure?</span><span class="sxs-lookup"><span data-stu-id="d77e7-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="d77e7-216">Sí.</span><span class="sxs-lookup"><span data-stu-id="d77e7-216">Yes.</span></span> <span data-ttu-id="d77e7-217">Este artículo se explica cómo toocreate tanto IPv4 como IPv6 invertir zonas de búsqueda DNS en el DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d77e7-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="d77e7-218">¿Puedo importar una zona de búsqueda inversa DNS existente?</span><span class="sxs-lookup"><span data-stu-id="d77e7-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="d77e7-219">Sí.</span><span class="sxs-lookup"><span data-stu-id="d77e7-219">Yes.</span></span> <span data-ttu-id="d77e7-220">Puede usar zonas DNS existentes de hello Azure CLI tooimport en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d77e7-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="d77e7-221">Esto funciona para las zonas de búsqueda directa y las zonas de búsqueda inversa.</span><span class="sxs-lookup"><span data-stu-id="d77e7-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="d77e7-222">Para obtener más información, consulte [importar y exportar un archivo de zona DNS mediante hello Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d77e7-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d77e7-223">Next steps</span></span>

<span data-ttu-id="d77e7-224">Para más información sobre los registros de DNS inverso, consulte información sobre la [búsqueda de DNS inverso en Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="d77e7-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="d77e7-225">Obtenga información acerca de cómo demasiado[administrar registros de DNS inverso para los servicios de Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="d77e7-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
