---
title: aaaManage DNS registra en DNS de Azure con PowerShell de Azure | Documentos de Microsoft
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
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="5a60c-104">Administración de conjuntos de registros y registros de DNS en Azure DNS mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a60c-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a60c-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5a60c-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="5a60c-106">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="5a60c-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="5a60c-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5a60c-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="5a60c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a60c-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="5a60c-109">Este artículo muestra cómo toomanage DNS los registros de la zona DNS mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a60c-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="5a60c-110">También se pueden administrar los registros de DNS mediante el uso de hello multiplataforma [CLI de Azure](dns-operations-recordsets-cli.md) o hello [portal de Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a60c-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="5a60c-111">ejemplos de Hello en este artículo se supone que ya está [instalado PowerShell de Azure, firmado y ha creado una zona DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="5a60c-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="5a60c-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="5a60c-112">Introduction</span></span>

<span data-ttu-id="5a60c-113">Antes de crear los registros DNS en DNS de Azure, primero debe toounderstand cómo Azure DNS organiza los registros DNS en conjuntos de registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="5a60c-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="5a60c-114">Para más información sobre los registros DNS en Azure DNS, consulte [DNS zones and records](dns-zones-records.md) (Zonas y registros DNS).</span><span class="sxs-lookup"><span data-stu-id="5a60c-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="5a60c-115">Creación de un nuevo registro DNS</span><span class="sxs-lookup"><span data-stu-id="5a60c-115">Create a new DNS record</span></span>

<span data-ttu-id="5a60c-116">Si el nuevo registro tiene Hola mismo nombre y tipo como un registro existente, deberá demasiado[Agregar conjunto de registros existente toohello](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="5a60c-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="5a60c-117">Si el nuevo registro tiene un tooall de nombre y tipo de diferentes registros existentes, deberá toocreate un nuevo conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="5a60c-118">Creación de registros "D" en un nuevo conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="5a60c-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="5a60c-119">Crear conjuntos de registros mediante hello `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5a60c-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="5a60c-120">Al crear un conjunto de registros, deberá nombre de conjunto de registros de hello toospecify, zona hello, hora de hello toolive (TTL), tipo de registro de Hola y Hola registros toobe creados.</span><span class="sxs-lookup"><span data-stu-id="5a60c-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="5a60c-121">parámetros de Hola para agregar el conjunto de registros tooa registros varían según tipo de Hola de conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="5a60c-122">Por ejemplo, cuando se utiliza un conjunto de registros de tipo 'A', necesitará dirección IP de hello toospecify mediante el parámetro hello `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="5a60c-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="5a60c-123">Para otros tipos de registros se usan otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="5a60c-124">Para más información, consulte [Ejemplos de tipos de registros adicionales](#additional-record-type-examples).</span><span class="sxs-lookup"><span data-stu-id="5a60c-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="5a60c-125">Hello en el ejemplo siguiente se crea un conjunto con nombre relativo Hola "www" en la zona DNS de 'contoso.com' hello de registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="5a60c-126">nombre completo de Hola de conjunto de registros de hello es 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="5a60c-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="5a60c-127">tipo de registro de Hello es 'A' y Hola TTL es 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="5a60c-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="5a60c-128">conjunto de registros de Hello contiene un único registro con la dirección IP '1.2.3.4'.</span><span class="sxs-lookup"><span data-stu-id="5a60c-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="5a60c-129">toocreate un conjunto de registros en hello 'vértice' de una zona (en este caso, "contoso.com"), usar el nombre de conjunto de registros de hello ' @' (excepto las comillas):</span><span class="sxs-lookup"><span data-stu-id="5a60c-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="5a60c-130">Si necesita toocreate un conjunto de registros que contiene más de un registro, crear una matriz local y agregar registros de Hola y después pasar la matriz de hello demasiado`New-AzureRmDnsRecordSet` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5a60c-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="5a60c-131">[Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="5a60c-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="5a60c-132">Hello en el ejemplo siguiente se muestra cómo toocreate un conjunto de registros con dos entradas de metadatos, ' departamento = finance' y ' entorno de producción de ='.</span><span class="sxs-lookup"><span data-stu-id="5a60c-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="5a60c-133">DNS de Azure también admite los conjuntos de registros 'empty', que pueden actuar como un marcador de posición tooreserve un nombre DNS antes de crear los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="5a60c-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="5a60c-134">Conjuntos de registros vacíos son visibles en el plano de control de hello DNS de Azure, pero aparecen en los servidores de nombres DNS de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="5a60c-135">Hola de ejemplo siguiente crea un conjunto de registros vacío:</span><span class="sxs-lookup"><span data-stu-id="5a60c-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="5a60c-136">Creación de registros de otros tipos</span><span class="sxs-lookup"><span data-stu-id="5a60c-136">Create records of other types</span></span>

<span data-ttu-id="5a60c-137">Después de ver en detalle cómo registros toocreate 'A', Hola siguientes ejemplos se muestra cómo toocreate registros de otros registran tipos compatibles con DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a60c-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="5a60c-138">En cada caso, le mostramos cómo toocreate un registro de conjunto que contiene un único registro.</span><span class="sxs-lookup"><span data-stu-id="5a60c-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="5a60c-139">Hello ejemplos anteriores para los registros 'A' pueden ser adaptado toocreate conjuntos de registros de otros tipos que contiene varios registros, con metadatos, o conjuntos de registros de toocreate vacía.</span><span class="sxs-lookup"><span data-stu-id="5a60c-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="5a60c-140">No damos un toocreate ejemplo un conjunto de registros SOA, ya que se crea SOA y eliminar con cada zona DNS y no puede crearse o eliminarse por separado.</span><span class="sxs-lookup"><span data-stu-id="5a60c-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="5a60c-141">Sin embargo, [Hola SOA se puede modificar, como se muestra en un ejemplo posterior](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="5a60c-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="5a60c-142">Creación de un conjunto de registros AAAA con un único registro</span><span class="sxs-lookup"><span data-stu-id="5a60c-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="5a60c-143">Creación de un conjunto de registros CNAME con un único registro</span><span class="sxs-lookup"><span data-stu-id="5a60c-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="5a60c-144">los estándares de DNS Hello no permiten registros CNAME en vértice Hola de una zona (`-Name '@'`), ni permiten a los conjuntos de registros que contiene más de un registro.</span><span class="sxs-lookup"><span data-stu-id="5a60c-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="5a60c-145">Para más información, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="5a60c-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="5a60c-146">Creación de un conjunto de registros MX con un único registro</span><span class="sxs-lookup"><span data-stu-id="5a60c-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="5a60c-147">En este ejemplo, se utiliza el nombre de conjunto de registros de hello ' @' registro toocreate un MX en vértice de la zona de hello (en este caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="5a60c-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="5a60c-148">Creación de un conjunto de registros NS con un único registro</span><span class="sxs-lookup"><span data-stu-id="5a60c-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="5a60c-149">Creación de un conjunto de registros PTR con un único registro</span><span class="sxs-lookup"><span data-stu-id="5a60c-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="5a60c-150">En este caso, ' Mi-arpa-zone.com' representa Hola zona de búsqueda inversa ARPA que representa el intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="5a60c-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="5a60c-151">Cada registro PTR establecida en esta zona corresponde tooan dirección IP dentro de este intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="5a60c-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="5a60c-152">Hola último octeto de la dirección IP de hello dentro de este intervalo IP representado por este registro es el nombre de registro de Hello '10'.</span><span class="sxs-lookup"><span data-stu-id="5a60c-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="5a60c-153">Creación de un conjunto de registros SRV con un único registro</span><span class="sxs-lookup"><span data-stu-id="5a60c-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="5a60c-154">Al crear un [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique hello  *\_servicio* y  *\_protocolo* Hola nombre de conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="5a60c-155">No hay ninguna necesidad de tooinclude ' @' Hola registro establece el nombre al crear un registro SRV en vértice de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="5a60c-156">Crear un conjunto de registros TXT con un único registro</span><span class="sxs-lookup"><span data-stu-id="5a60c-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="5a60c-157">Hello en el ejemplo siguiente se muestra cómo registrar toocreate TXT.</span><span class="sxs-lookup"><span data-stu-id="5a60c-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="5a60c-158">Para obtener más información acerca de la longitud de cadena máxima Hola admitida en registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="5a60c-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="5a60c-159">Recuperación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="5a60c-159">Get a record set</span></span>

<span data-ttu-id="5a60c-160">tooretrieve un conjunto de registros existente, utilice `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="5a60c-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="5a60c-161">Este cmdlet devuelve un objeto local que representa Hola conjunto de registros de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a60c-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="5a60c-162">Al igual que con `New-AzureRmDnsRecordSet`, debe ser el nombre de conjunto de registros de hello dado un *relativa* nombre, lo que significa que debe excluir el nombre de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="5a60c-163">También necesitará toospecify tipo de registro de hello y zona de Hola que contiene el conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="5a60c-164">Hello en el ejemplo siguiente se muestra cómo tooretrieve un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="5a60c-165">En este ejemplo, la zona de Hola se especifica utilizando hello `-ZoneName` y `-ResourceGroupName` parámetros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="5a60c-166">Como alternativa, también puede especificar zona de hello mediante un objeto de zona que se pasan mediante hello `-Zone` parámetro.</span><span class="sxs-lookup"><span data-stu-id="5a60c-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="5a60c-167">Enumeración de conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="5a60c-167">List record sets</span></span>

<span data-ttu-id="5a60c-168">También puede usar `Get-AzureRmDnsZone` conjuntos de registros de toolist en una zona, mediante la omisión de hello `-Name` o `-RecordType` parámetros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="5a60c-169">Hello en el ejemplo siguiente se devuelve todos los registros se establece en la zona de hello:</span><span class="sxs-lookup"><span data-stu-id="5a60c-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="5a60c-170">Hello en el ejemplo siguiente se muestra cómo todos los conjuntos de un tipo determinado de registros se puede recuperar mediante la especificación de tipo de registro de Hola durante la omisión de registro de hello establece nombre:</span><span class="sxs-lookup"><span data-stu-id="5a60c-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="5a60c-171">tooretrieve establece todos los registros con un nombre específico, a través de los tipos de registro, deberá tooretrieve todos los conjuntos de registros y, a continuación, resultados del filtro hello:</span><span class="sxs-lookup"><span data-stu-id="5a60c-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="5a60c-172">En Hola a todos los ejemplos precedentes Hola zona puede especificar mediante el uso de Hola `-ZoneName` y `-ResourceGroupName`parámetros (como se muestra), o mediante la especificación de un objeto de zona:</span><span class="sxs-lookup"><span data-stu-id="5a60c-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="5a60c-173">Agregar un registro tooan existente de conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="5a60c-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="5a60c-174">conjunto de tooadd un registro existente de registro tooan, siga Hola siga tres pasos:</span><span class="sxs-lookup"><span data-stu-id="5a60c-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="5a60c-175">Obtener el conjunto de registros existente Hola</span><span class="sxs-lookup"><span data-stu-id="5a60c-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="5a60c-176">Agregar Hola nuevo registro toohello local conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="5a60c-177">Esta operación se realiza sin conexión.</span><span class="sxs-lookup"><span data-stu-id="5a60c-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="5a60c-178">Confirmar Hola cambio posterior toohello servicio DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a60c-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="5a60c-179">Usar `Set-AzureRmDnsRecordSet` *reemplaza* Hola existente conjunto de registros de DNS de Azure (y todos los registros que lo contiene) con el conjunto de registros de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="5a60c-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="5a60c-180">[Comprobaciones de eTag](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se sobrescriben.</span><span class="sxs-lookup"><span data-stu-id="5a60c-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="5a60c-181">Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="5a60c-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="5a60c-182">Esta secuencia de operaciones también puede ser *canaliza*, lo que significa que se pasa el objeto de conjunto de registros de hello mediante canalización hello, en lugar de pasarlo como un parámetro:</span><span class="sxs-lookup"><span data-stu-id="5a60c-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="5a60c-183">ejemplos de Hello anteriores muestran cómo establece tooadd un registro existente de 'A' tooan registros de tipo 'A'.</span><span class="sxs-lookup"><span data-stu-id="5a60c-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="5a60c-184">Una secuencia de operaciones similar está tooadd usa registros toorecord conjuntos de otros tipos, sustituyendo hello `-Ipv4Address` parámetro de `Add-AzureRmDnsRecordConfig` con otro tipo de registro de tooeach específico de parámetros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="5a60c-185">Hello parámetros para cada tipo de registro se Hola igual que para hello `New-AzureRmDnsRecordConfig` cmdlet, tal y como se muestra en [ejemplos adicionales de tipo de registro](#additional-record-type-examples) anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5a60c-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="5a60c-186">Los conjuntos de registros de tipo "CNAME" o "SOA" no pueden contener más de un registro.</span><span class="sxs-lookup"><span data-stu-id="5a60c-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="5a60c-187">Esta restricción surge de los estándares de DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="5a60c-188">No es una limitación de Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="5a60c-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="5a60c-189">Eliminación de un registro de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="5a60c-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="5a60c-190">Hola proceso tooremove un registro de un conjunto de registros es similar tooadd de proceso de toohello un registro tooan existente grabar conjunto:</span><span class="sxs-lookup"><span data-stu-id="5a60c-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="5a60c-191">Obtener el conjunto de registros existente Hola</span><span class="sxs-lookup"><span data-stu-id="5a60c-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="5a60c-192">Quitar el registro de hello de objeto de conjunto de registros local Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="5a60c-193">Esta operación se realiza sin conexión.</span><span class="sxs-lookup"><span data-stu-id="5a60c-193">This is an off-line operation.</span></span> <span data-ttu-id="5a60c-194">registro de Hello que se va a quitar debe ser una coincidencia exacta con un registro existente en todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="5a60c-195">Confirmar Hola cambio posterior toohello servicio DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a60c-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="5a60c-196">Hola de uso opcional `-Overwrite` cambiar toosuppress [Etag comprueba](dns-zones-records.md#etags) para cambios simultáneos.</span><span class="sxs-lookup"><span data-stu-id="5a60c-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="5a60c-197">Hola anteriormente las último registro de hello del tooremove de secuencia de un conjunto de registros de uso no elimina el conjunto de registros de hello, en su lugar deja un conjunto de registros vacío.</span><span class="sxs-lookup"><span data-stu-id="5a60c-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="5a60c-198">tooremove un conjunto de registros por completo, vea [eliminar un conjunto de registros](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="5a60c-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="5a60c-199">De igual forma tooadding registros tooa conjunto de registros, secuencia de Hola de tooremove operaciones también se puede canalizar un conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="5a60c-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="5a60c-200">Se admiten diferentes tipos de registros al pasar parámetros específicos del tipo adecuado de hello demasiado`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="5a60c-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="5a60c-201">Hello parámetros para cada tipo de registro se Hola igual que para hello `New-AzureRmDnsRecordConfig` cmdlet, tal y como se muestra en [ejemplos adicionales de tipo de registro](#additional-record-type-examples) anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5a60c-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="5a60c-202">Modificación de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="5a60c-202">Modify an existing record set</span></span>

<span data-ttu-id="5a60c-203">Hola los pasos para modificar un conjunto de registros existente son similares toohello pasos que seguir al agregar o quitar los registros de un conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="5a60c-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="5a60c-204">Recuperar registro existente de hello establecer mediante `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="5a60c-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="5a60c-205">Modifique el objeto de conjunto de registros local Hola por:</span><span class="sxs-lookup"><span data-stu-id="5a60c-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="5a60c-206">Agregue o quite registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-206">Adding or removing records</span></span>
    * <span data-ttu-id="5a60c-207">Cambiar los parámetros de Hola de registros existentes</span><span class="sxs-lookup"><span data-stu-id="5a60c-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="5a60c-208">Cambiar el registro de hello del conjunto de metadatos y la hora toolive (TTL)</span><span class="sxs-lookup"><span data-stu-id="5a60c-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="5a60c-209">Confirmar cambios mediante el uso de hello `Set-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5a60c-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="5a60c-210">Esto *reemplaza* Hola existente conjunto de registros de DNS de Azure con el conjunto de registros de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="5a60c-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="5a60c-211">Cuando se usa `Set-AzureRmDnsRecordSet`, [Etag comprueba](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se sobrescriben.</span><span class="sxs-lookup"><span data-stu-id="5a60c-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="5a60c-212">Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="5a60c-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="5a60c-213">establece tooupdate un registro en un registro existente</span><span class="sxs-lookup"><span data-stu-id="5a60c-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="5a60c-214">En este ejemplo, cambiamos la dirección IP de Hola de un registro "A" existente:</span><span class="sxs-lookup"><span data-stu-id="5a60c-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="5a60c-215">toomodify un registro SOA</span><span class="sxs-lookup"><span data-stu-id="5a60c-215">toomodify an SOA record</span></span>

<span data-ttu-id="5a60c-216">No se puede agregar o quitar registros de hello creado automáticamente el registro SOA establecido en vértice de la zona de hello (`-Name "@"`, incluidas las comillas).</span><span class="sxs-lookup"><span data-stu-id="5a60c-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="5a60c-217">Sin embargo, puede modificar cualquiera de los parámetros de hello en hello registro SOA (excepto el "Host") y registro de hello establecer TTL.</span><span class="sxs-lookup"><span data-stu-id="5a60c-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="5a60c-218">Hola siguiente ejemplo se muestra cómo hello toochange *correo electrónico* propiedad de hello registro SOA:</span><span class="sxs-lookup"><span data-stu-id="5a60c-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="5a60c-219">registros de toomodify NS en vértice de la zona de Hola</span><span class="sxs-lookup"><span data-stu-id="5a60c-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="5a60c-220">registro de NS de Hello establecido en vértice de la zona de Hola se crea automáticamente con cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="5a60c-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="5a60c-221">Contiene los nombres de Hola de zona de hello Azure DNS nombre servidores toohello asignado.</span><span class="sxs-lookup"><span data-stu-id="5a60c-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="5a60c-222">Puede agregar nombre adicionales servidores toothis NS conjunto de registros, toosupport alojar conjuntamente dominios con más de un proveedor DNS.</span><span class="sxs-lookup"><span data-stu-id="5a60c-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="5a60c-223">También puede modificar Hola TTL y los metadatos para este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="5a60c-224">Sin embargo, no se puede quitar o modificar servidores de nombres DNS de Azure previamente rellenados Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="5a60c-225">Tenga en cuenta que esto se aplica solo toohello NS conjunto de registros en vértice de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="5a60c-226">Otros conjuntos de registros NS en su zona (como las zonas secundarias de toodelegate usado) pueden modificarse sin restricción.</span><span class="sxs-lookup"><span data-stu-id="5a60c-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="5a60c-227">Hola de ejemplo siguiente muestra cómo tooadd establece de un registro de NS de toohello de servidor de nombres adicionales en vértice de la zona de hello:</span><span class="sxs-lookup"><span data-stu-id="5a60c-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="5a60c-228">metadatos de conjunto de registros de toomodify</span><span class="sxs-lookup"><span data-stu-id="5a60c-228">toomodify record set metadata</span></span>

<span data-ttu-id="5a60c-229">[Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="5a60c-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="5a60c-230">Hello en el ejemplo siguiente se muestra cómo establecen toomodify Hola metadatos de un registro existente:</span><span class="sxs-lookup"><span data-stu-id="5a60c-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="5a60c-231">Eliminación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="5a60c-231">Delete a record set</span></span>

<span data-ttu-id="5a60c-232">Conjuntos de registros pueden eliminarse mediante el uso de hello `Remove-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5a60c-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="5a60c-233">Eliminación de un conjunto de registros, también elimina todas las entradas de conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="5a60c-234">No se puede eliminar Hola SOA y NS conjuntos de registros en vértice de la zona de hello (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="5a60c-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="5a60c-235">DNS de Azure crea estos operación automáticamente cuando zona Hola se creó y elimina automáticamente cuando se elimina la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a60c-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="5a60c-236">Hello en el ejemplo siguiente se muestra cómo toodelete un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="5a60c-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="5a60c-237">En este ejemplo, el nombre del conjunto de registros de hello, tipo de conjunto de registros, nombre de la zona y grupo de recursos se cada especifican explícitamente.</span><span class="sxs-lookup"><span data-stu-id="5a60c-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="5a60c-238">Como alternativa, se puede especificar el conjunto de registros de Hola por nombre y tipo, y Hola especificados mediante un objeto de la zona:</span><span class="sxs-lookup"><span data-stu-id="5a60c-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="5a60c-239">Como una tercera opción propio conjunto de registros de hello pueden especificarse mediante un objeto de conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="5a60c-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="5a60c-240">Cuando se especifica toobe eliminada mediante el uso de un objeto de conjunto de registros de conjunto de registros de hello [Etag comprueba](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se eliminan.</span><span class="sxs-lookup"><span data-stu-id="5a60c-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="5a60c-241">Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="5a60c-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="5a60c-242">También se puede canalizar el objeto de conjunto de registros de Hello en lugar de que se pasa como parámetro:</span><span class="sxs-lookup"><span data-stu-id="5a60c-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="5a60c-243">Mensajes de confirmación</span><span class="sxs-lookup"><span data-stu-id="5a60c-243">Confirmation prompts</span></span>

<span data-ttu-id="5a60c-244">Hola `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, y `Remove-AzureRmDnsRecordSet` todos los cmdlets admiten mensajes de confirmación.</span><span class="sxs-lookup"><span data-stu-id="5a60c-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="5a60c-245">Cada cmdlet pide confirmación si hello `$ConfirmPreference` variable de preferencia de PowerShell tiene un valor de `Medium` o inferior.</span><span class="sxs-lookup"><span data-stu-id="5a60c-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="5a60c-246">Desde el valor predeterminado de Hola para `$ConfirmPreference` es `High`, esos mensajes no tienen al usar la configuración de PowerShell de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5a60c-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="5a60c-247">Puede invalidar Hola actual `$ConfirmPreference` configuración mediante hello `-Confirm` parámetro.</span><span class="sxs-lookup"><span data-stu-id="5a60c-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="5a60c-248">Si especifica `-Confirm` o `-Confirm:$True` , Hola cmdlet solicita confirmación antes de que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="5a60c-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="5a60c-249">Si especifica `-Confirm:$False` , Hola cmdlet no pide confirmación.</span><span class="sxs-lookup"><span data-stu-id="5a60c-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="5a60c-250">Para más información sobre `-Confirm` y `$ConfirmPreference`, consulte [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Acerca de las variables de preferencias).</span><span class="sxs-lookup"><span data-stu-id="5a60c-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a60c-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a60c-251">Next steps</span></span>

<span data-ttu-id="5a60c-252">Más información sobre [zonas y registros en Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="5a60c-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="5a60c-253">Obtenga información acerca de cómo demasiado[proteger sus zonas y registros](dns-protect-zones-recordsets.md) cuando se usa DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a60c-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="5a60c-254">Hola de revisión [documentación de referencia de PowerShell de DNS de Azure](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="5a60c-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
