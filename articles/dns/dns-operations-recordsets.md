---
title: "Administración de registros DNS en Azure DNS mediante Azure PowerShell | Microsoft Docs"
description: "Administración de conjuntos de registros y registros DNS en DNS de Azure al hospedar dominios en DNS de Azure. Todos los comandos de PowerShell para operaciones en conjuntos de registros y registros."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="6d784-104">Administración de conjuntos de registros y registros de DNS en Azure DNS mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d784-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d784-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6d784-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="6d784-106">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6d784-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="6d784-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6d784-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="6d784-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d784-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="6d784-109">En este artículo se muestra cómo administrar registros DNS para su zona DNS mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d784-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="6d784-110">Los registros de DNS también se pueden administrar mediante la [CLI de Azure](dns-operations-recordsets-cli.md) multiplataforma o [Azure Portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6d784-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="6d784-111">En los ejemplos de este artículo se supone que ya ha [instalado Azure PowerShell, iniciado sesión y creado una zona DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="6d784-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="6d784-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="6d784-112">Introduction</span></span>

<span data-ttu-id="6d784-113">Antes de crear registros DNS en Azure DNS, es necesario que comprenda cómo Azure DNS los organiza en conjuntos de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="6d784-114">Para más información sobre los registros DNS en Azure DNS, consulte [DNS zones and records](dns-zones-records.md) (Zonas y registros DNS).</span><span class="sxs-lookup"><span data-stu-id="6d784-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="6d784-115">Creación de un nuevo registro DNS</span><span class="sxs-lookup"><span data-stu-id="6d784-115">Create a new DNS record</span></span>

<span data-ttu-id="6d784-116">Si el nuevo registro tiene el mismo nombre y tipo que un registro existente, debe [agregarlo al conjunto de registros existente](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="6d784-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="6d784-117">Si el nuevo registro tiene un nombre y un tipo diferentes al de todos los registros existentes, debe crear un nuevo conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="6d784-118">Creación de registros "D" en un nuevo conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="6d784-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="6d784-119">Los conjuntos de registros se crean mediante el cmdlet `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="6d784-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="6d784-120">Al crear un conjunto de registros, deberá especificar el nombre del conjunto de registros, la zona, el período de vida (TTL), el tipo de registro y los registros que se crearán.</span><span class="sxs-lookup"><span data-stu-id="6d784-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="6d784-121">Los parámetros para agregar registros a un conjunto de registros varían según el tipo de conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="6d784-122">Por ejemplo, cuando se usa un conjunto de registros de tipo "A", deberá especificar la dirección IP mediante el parámetro `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="6d784-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="6d784-123">Para otros tipos de registros se usan otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="6d784-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="6d784-124">Para más información, consulte [Ejemplos de tipos de registros adicionales](#additional-record-type-examples).</span><span class="sxs-lookup"><span data-stu-id="6d784-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="6d784-125">En el ejemplo siguiente se crea un conjunto de registros con el nombre relativo "www" en la zona DNS "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="6d784-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="6d784-126">El nombre completo del conjunto de registros es www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6d784-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="6d784-127">El tipo de registro es "D" y el valor de TTL es de 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="6d784-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="6d784-128">El conjunto de registros contiene un único registro con la dirección IP "1.2.3.4".</span><span class="sxs-lookup"><span data-stu-id="6d784-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="6d784-129">Para crear un conjunto de registros en el "vértice" de una zona (en este caso, "contoso.com"), use el nombre del conjunto de registros "@" (excluidas las comillas):</span><span class="sxs-lookup"><span data-stu-id="6d784-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="6d784-130">Si necesita crear un conjunto de registros que contenga más de un registro, primero cree una matriz local y agregue los registros, luego pase la matriz a `New-AzureRmDnsRecordSet` de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="6d784-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="6d784-131">Se pueden usar [metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) para asociar datos específicos de la aplicación con cada conjunto de registros como pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="6d784-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="6d784-132">En el ejemplo siguiente se muestra cómo crear un conjunto de registros con dos entradas de metadatos: "dept=finance" y "environment=production".</span><span class="sxs-lookup"><span data-stu-id="6d784-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="6d784-133">Azure DNS también admite conjuntos de registros "vacíos" que pueden funcionar como marcador de posición para reservar un nombre DNS antes de crear registros DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="6d784-134">Los conjuntos de registros vacíos son visibles en el panel de control de Azure DNS, pero aparecen en los servidores de nombres de Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="6d784-135">En el ejemplo siguiente se crea un conjunto de registros vacío:</span><span class="sxs-lookup"><span data-stu-id="6d784-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="6d784-136">Creación de registros de otros tipos</span><span class="sxs-lookup"><span data-stu-id="6d784-136">Create records of other types</span></span>

<span data-ttu-id="6d784-137">Después de haber visto de forma detallada como crear registros "A", en los siguientes ejemplos se muestra cómo crear registros de otros tipos compatibles con Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="6d784-138">En cada caso, se muestra cómo crear un nuevo conjunto de registros que contiene un único registro.</span><span class="sxs-lookup"><span data-stu-id="6d784-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="6d784-139">Los ejemplos anteriores para registros "A" se pueden adaptar para crear conjuntos de registros de otros tipos que contengan varios registros, con metadatos, o crear conjuntos de registros vacíos.</span><span class="sxs-lookup"><span data-stu-id="6d784-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="6d784-140">No se proporciona un ejemplo para crear un conjunto de registros SOA, dado que los registros SOA se crean y eliminan con cada zona de DNS y no lo pueden hacer por separado.</span><span class="sxs-lookup"><span data-stu-id="6d784-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="6d784-141">Sin embargo, [el registro SOA se puede modificar, como se muestra en un ejemplo más adelante](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="6d784-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="6d784-142">Creación de un conjunto de registros AAAA con un único registro</span><span class="sxs-lookup"><span data-stu-id="6d784-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="6d784-143">Creación de un conjunto de registros CNAME con un único registro</span><span class="sxs-lookup"><span data-stu-id="6d784-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="6d784-144">Los estándares DNS no permiten registros CNAME en el vértice de una zona (`-Name '@'`), ni permiten conjuntos de registros que contengan más de un registro.</span><span class="sxs-lookup"><span data-stu-id="6d784-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="6d784-145">Para más información, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="6d784-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="6d784-146">Creación de un conjunto de registros MX con un único registro</span><span class="sxs-lookup"><span data-stu-id="6d784-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="6d784-147">En este ejemplo, se utiliza el nombre de conjunto de registros "@" para crear el registro MX en el vértice de la zona (por ejemplo, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="6d784-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="6d784-148">Creación de un conjunto de registros NS con un único registro</span><span class="sxs-lookup"><span data-stu-id="6d784-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="6d784-149">Creación de un conjunto de registros PTR con un único registro</span><span class="sxs-lookup"><span data-stu-id="6d784-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="6d784-150">En este caso, "my-arpa-zone.com" representa la zona de búsqueda inversa ARPA que representa el intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="6d784-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="6d784-151">Cada registro PTR establecido en esta zona se corresponde con una dirección IP dentro de este intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="6d784-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="6d784-152">El nombre de registro "10" es el último octeto de la dirección IP dentro del intervalo IP que representa dicho registro.</span><span class="sxs-lookup"><span data-stu-id="6d784-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="6d784-153">Creación de un conjunto de registros SRV con un único registro</span><span class="sxs-lookup"><span data-stu-id="6d784-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="6d784-154">Al crear un [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique el *\_servicio* y el *\_protocolo* en el nombre del conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="6d784-155">No es necesario incluir "@" en el nombre del conjunto de registros al crear un conjunto de registros SRV en el vértice de la zona.</span><span class="sxs-lookup"><span data-stu-id="6d784-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="6d784-156">Crear un conjunto de registros TXT con un único registro</span><span class="sxs-lookup"><span data-stu-id="6d784-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="6d784-157">En el ejemplo siguiente se muestra cómo crear un registro TXT.</span><span class="sxs-lookup"><span data-stu-id="6d784-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="6d784-158">Para más información sobre la longitud de cadena máxima admitida en registros TXT, consulte [Registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="6d784-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="6d784-159">Recuperación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="6d784-159">Get a record set</span></span>

<span data-ttu-id="6d784-160">Para recuperar un conjunto de registros existente, use `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="6d784-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="6d784-161">Este cmdlet devuelve un objeto local que representa el conjunto de registros en Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="6d784-162">Al igual que con `New-AzureRmDnsRecordSet`, el nombre del conjunto de registros dado debe ser un nombre *relativo*, lo que significa que debe excluir el nombre de zona.</span><span class="sxs-lookup"><span data-stu-id="6d784-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="6d784-163">También se debe especificar el tipo de registro y la zona que contiene el conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="6d784-164">En el ejemplo siguiente se muestra cómo recuperar un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="6d784-165">En este ejemplo, la zona se especifica mediante los parámetros `-ZoneName` y `-ResourceGroupName`.</span><span class="sxs-lookup"><span data-stu-id="6d784-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6d784-166">Como alternativa, también puede especificar la zona mediante un objeto de zona, que se pasa mediante el parámetro `-Zone`.</span><span class="sxs-lookup"><span data-stu-id="6d784-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="6d784-167">Enumeración de conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="6d784-167">List record sets</span></span>

<span data-ttu-id="6d784-168">También puede usar `Get-AzureRmDnsZone` para mostrar conjuntos de registros de una zona y omitir los parámetros `-Name` o `-RecordType`.</span><span class="sxs-lookup"><span data-stu-id="6d784-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="6d784-169">En el ejemplo siguiente se devuelven todos los conjuntos de registros de la zona:</span><span class="sxs-lookup"><span data-stu-id="6d784-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6d784-170">En el ejemplo siguiente se muestra cómo se pueden recuperar todos los conjuntos de registros de un tipo dado mediante la especificación del tipo de registro y la omisión del nombre del conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="6d784-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6d784-171">Para recuperar todos los conjuntos de registros con un nombre específico de todos los tipos de registros, debe recuperar todos los conjuntos de registros y luego filtrar los resultados:</span><span class="sxs-lookup"><span data-stu-id="6d784-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="6d784-172">En todos los ejemplos anteriores, la zona se puede especificar mediante los parámetros `-ZoneName` y `-ResourceGroupName` (como se muestra) o por medio de un objeto de zona:</span><span class="sxs-lookup"><span data-stu-id="6d784-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="6d784-173">Adición de un registro a un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="6d784-173">Add a record to an existing record set</span></span>

<span data-ttu-id="6d784-174">Para agregar un registro a un conjunto de registros existente, siga estos tres pasos:</span><span class="sxs-lookup"><span data-stu-id="6d784-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="6d784-175">Obtenga el conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="6d784-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="6d784-176">Agregue el nuevo registro al conjunto de registros local.</span><span class="sxs-lookup"><span data-stu-id="6d784-176">Add the new record to the local record set.</span></span> <span data-ttu-id="6d784-177">Esta operación se realiza sin conexión.</span><span class="sxs-lookup"><span data-stu-id="6d784-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="6d784-178">Confirme el cambio al servicio Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="6d784-179">Al usar `Set-AzureRmDnsRecordSet` *, se sustituye* el conjunto de registros existente en Azure DNS (y todos los registros que contiene) por el conjunto de registros especificado.</span><span class="sxs-lookup"><span data-stu-id="6d784-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="6d784-180">Se usan [comprobaciones de ETag](dns-zones-records.md#etags) para garantizar que los cambios simultáneos no se sobrescriban.</span><span class="sxs-lookup"><span data-stu-id="6d784-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="6d784-181">Puede usar el modificador `-Overwrite` opcional para suprimir estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="6d784-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="6d784-182">Esta secuencia de operaciones también se puede *canalizar*, es decir, pasar el objeto de conjunto de registros mediante la canalización en lugar de como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="6d784-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="6d784-183">Los ejemplos anteriores muestran cómo agregar un registro "A" a un conjunto de registros existente de tipo "A".</span><span class="sxs-lookup"><span data-stu-id="6d784-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="6d784-184">Se usa una secuencia parecida de operaciones para agregar registros a conjunto de registros de otros tipos, sustituyendo el parámetro `-Ipv4Address` de `Add-AzureRmDnsRecordConfig` por otros parámetros específicos de cada tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="6d784-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="6d784-185">Los parámetros de cada tipo de registro son los mismos que para el cmdlet `New-AzureRmDnsRecordConfig`, como se muestra en [Ejemplos de tipos de registros adicionales](#additional-record-type-examples) anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6d784-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="6d784-186">Los conjuntos de registros de tipo "CNAME" o "SOA" no pueden contener más de un registro.</span><span class="sxs-lookup"><span data-stu-id="6d784-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="6d784-187">Esta restricción surge de los estándares de DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="6d784-188">No es una limitación de Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="6d784-189">Eliminación de un registro de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="6d784-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="6d784-190">El proceso para quitar un registro de un conjunto de registros es similar al proceso para agregar un registro a un conjunto de registros existente:</span><span class="sxs-lookup"><span data-stu-id="6d784-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="6d784-191">Obtenga el conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="6d784-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="6d784-192">Quite el registro del objeto del conjunto de registros local.</span><span class="sxs-lookup"><span data-stu-id="6d784-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="6d784-193">Esta operación se realiza sin conexión.</span><span class="sxs-lookup"><span data-stu-id="6d784-193">This is an off-line operation.</span></span> <span data-ttu-id="6d784-194">Todos los parámetros del registro que se va a eliminar deben coincidir exactamente con los del registro existente.</span><span class="sxs-lookup"><span data-stu-id="6d784-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="6d784-195">Confirme el cambio al servicio Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="6d784-196">Use el modificador `-Overwrite` para suprimir las [comprobaciones de ETag](dns-zones-records.md#etags) para cambios simultáneos.</span><span class="sxs-lookup"><span data-stu-id="6d784-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="6d784-197">El uso de la secuencia anterior para quitar el último registro de un conjunto de registros no elimina el conjunto de registros, sino que deja un conjunto de registros vacío.</span><span class="sxs-lookup"><span data-stu-id="6d784-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="6d784-198">Para quitar completamente un conjunto de registros, consulte [Eliminación de un conjunto de registros](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="6d784-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="6d784-199">Lo mismo que para agregar registros a un conjunto de registros, la secuencia de operaciones para quitar un conjunto de registros también se puede canalizar:</span><span class="sxs-lookup"><span data-stu-id="6d784-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="6d784-200">Se admiten diferentes tipos de registros pasando los parámetros adecuados específicos del tipo a `Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="6d784-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="6d784-201">Los parámetros de cada tipo de registro son los mismos que para el cmdlet `New-AzureRmDnsRecordConfig`, como se muestra en [Ejemplos de tipos de registros adicionales](#additional-record-type-examples) anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6d784-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="6d784-202">Modificación de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="6d784-202">Modify an existing record set</span></span>

<span data-ttu-id="6d784-203">Los pasos para modificar un conjunto de registros existente son parecidos a los que se realizan al agregar o quitar registros de un conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="6d784-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="6d784-204">Recupere el conjunto de registros existente mediante `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="6d784-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="6d784-205">Para modificar el objeto de conjunto de registros local:</span><span class="sxs-lookup"><span data-stu-id="6d784-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="6d784-206">Agregue o quite registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-206">Adding or removing records</span></span>
    * <span data-ttu-id="6d784-207">Cambie los parámetros de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="6d784-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="6d784-208">Cambie los metadatos del conjunto de registros y el período de vida (TTL).</span><span class="sxs-lookup"><span data-stu-id="6d784-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="6d784-209">Confirme los cambios mediante el cmdlet `Set-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="6d784-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="6d784-210">Esta acción *reemplaza* el conjunto de registros existente de Azure DNS por el conjunto de registros especificado.</span><span class="sxs-lookup"><span data-stu-id="6d784-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="6d784-211">Al usar `Set-AzureRmDnsRecordSet`, se emplean [comprobaciones de ETag](dns-zones-records.md#etags) para garantizar que los cambios simultáneos no se sobrescriban.</span><span class="sxs-lookup"><span data-stu-id="6d784-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="6d784-212">Puede usar el modificador `-Overwrite` opcional para suprimir estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="6d784-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="6d784-213">Para actualizar un registro en un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="6d784-213">To update a record in an existing record set</span></span>

<span data-ttu-id="6d784-214">En este ejemplo, se cambiará la dirección IP de un registro A existente:</span><span class="sxs-lookup"><span data-stu-id="6d784-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="6d784-215">Para modificar un registro SOA</span><span class="sxs-lookup"><span data-stu-id="6d784-215">To modify an SOA record</span></span>

<span data-ttu-id="6d784-216">No puede agregar ni quitar registros del conjunto de registros SOA creado automáticamente en el vértice de zona (`-Name "@"`, comillas incluidas).</span><span class="sxs-lookup"><span data-stu-id="6d784-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="6d784-217">Sin embargo, puede modificar cualquiera de los parámetros del registro SOA (excepto "Host") y del conjunto de registros TTL.</span><span class="sxs-lookup"><span data-stu-id="6d784-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="6d784-218">En el ejemplo siguiente se muestra cómo cambiar la propiedad *Email* del registro SOA:</span><span class="sxs-lookup"><span data-stu-id="6d784-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="6d784-219">Para modificar los registros NS en el vértice de zona</span><span class="sxs-lookup"><span data-stu-id="6d784-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="6d784-220">El conjunto de registros NS en el vértice de zona se crea automáticamente con cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="6d784-221">Este conjunto de registros contiene los nombres de los servidores de nombres de Azure DNS asignados a la zona.</span><span class="sxs-lookup"><span data-stu-id="6d784-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="6d784-222">Puede agregar más servidores de nombres a este conjunto de registros NS, para admitir dominios de hospedaje conjunto con más de un proveedor DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="6d784-223">También puede modificar el TTL y los metadatos de este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="6d784-224">Sin embargo, no puede quitar ni modificar los servidores de nombres de Azure DNS rellenados previamente.</span><span class="sxs-lookup"><span data-stu-id="6d784-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="6d784-225">Tenga en cuenta que esto solo se aplica al conjunto de registros NS en el vértice de zona.</span><span class="sxs-lookup"><span data-stu-id="6d784-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="6d784-226">Otros conjuntos de registros NS de su zona (como los que se usan para delegar zonas secundarias) se pueden modificar sin restricciones.</span><span class="sxs-lookup"><span data-stu-id="6d784-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="6d784-227">En el ejemplo siguiente se muestra cómo agregar un servidor de nombres adicional al conjunto de registros NS en el vértice de zona:</span><span class="sxs-lookup"><span data-stu-id="6d784-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="6d784-228">Para modificar los metadatos del conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="6d784-228">To modify record set metadata</span></span>

<span data-ttu-id="6d784-229">Se pueden usar [metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) para asociar datos específicos de la aplicación con cada conjunto de registros como pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="6d784-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="6d784-230">En el ejemplo siguiente se muestra cómo modificar los metadatos de un conjunto de registros existente:</span><span class="sxs-lookup"><span data-stu-id="6d784-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="6d784-231">Eliminación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="6d784-231">Delete a record set</span></span>

<span data-ttu-id="6d784-232">Los conjuntos de registros pueden eliminarse mediante el cmdlet `Remove-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="6d784-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="6d784-233">Al eliminar un conjunto de registros también se eliminan todos los registros que contiene.</span><span class="sxs-lookup"><span data-stu-id="6d784-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="6d784-234">No se pueden eliminar los conjuntos de registros SOA y NS en el vértice de zona (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="6d784-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="6d784-235">Los DNS de Azure se crean automáticamente cuando se genera la zona y se eliminan automáticamente cuando se elimina.</span><span class="sxs-lookup"><span data-stu-id="6d784-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="6d784-236">En el ejemplo siguiente se muestra cómo eliminar un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="6d784-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="6d784-237">En este ejemplo, el nombre del conjunto de registros, el tipo de conjunto de registros, el nombre de zona y el grupo de recursos se especifican de manera explícita.</span><span class="sxs-lookup"><span data-stu-id="6d784-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6d784-238">Como alternativa, el conjunto de registros se puede especificar por nombre y tipo, y la zona se puede especificar mediante un objeto:</span><span class="sxs-lookup"><span data-stu-id="6d784-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="6d784-239">Como tercera opción, el propio conjunto de registros se puede especificar mediante un objeto de conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="6d784-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="6d784-240">Cuando se especifica el conjunto de registros que se va a eliminar mediante un objeto de conjunto de registros, se usan [comprobaciones de ETag](dns-zones-records.md#etags) para garantizar que no se eliminan los cambios simultáneos.</span><span class="sxs-lookup"><span data-stu-id="6d784-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="6d784-241">Puede usar el modificador `-Overwrite` opcional para suprimir estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="6d784-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="6d784-242">El objeto del conjunto de registros también puede canalizarse en lugar de pasarse como un parámetro:</span><span class="sxs-lookup"><span data-stu-id="6d784-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="6d784-243">Mensajes de confirmación</span><span class="sxs-lookup"><span data-stu-id="6d784-243">Confirmation prompts</span></span>

<span data-ttu-id="6d784-244">Los cmdlets `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet` y `Remove-AzureRmDnsRecordSet` todos admiten mensajes de confirmación.</span><span class="sxs-lookup"><span data-stu-id="6d784-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="6d784-245">Cada cmdlet pide confirmación si la variable de preferencia de PowerShell `$ConfirmPreference` tiene un valor de `Medium` o inferior.</span><span class="sxs-lookup"><span data-stu-id="6d784-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="6d784-246">Dado que el valor predeterminado de `$ConfirmPreference` es `High`, estos mensajes no se proporcionan cuando se usa la configuración predeterminada de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d784-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="6d784-247">Puede invalidar el valor actual de `$ConfirmPreference` mediante el parámetro `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="6d784-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="6d784-248">Si especifica `-Confirm` o `-Confirm:$True`, el cmdlet solicita confirmación antes de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="6d784-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="6d784-249">Si especifica `-Confirm:$False`, el cmdlet no solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="6d784-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="6d784-250">Para más información sobre `-Confirm` y `$ConfirmPreference`, consulte [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Acerca de las variables de preferencias).</span><span class="sxs-lookup"><span data-stu-id="6d784-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d784-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d784-251">Next steps</span></span>

<span data-ttu-id="6d784-252">Más información sobre [zonas y registros en Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="6d784-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="6d784-253">Aprenda a [proteger las zonas y los registros](dns-protect-zones-recordsets.md) cuando se usa Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6d784-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="6d784-254">Revise la [documentación de referencia de PowerShell para Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="6d784-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
