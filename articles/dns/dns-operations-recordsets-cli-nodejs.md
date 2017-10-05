---
title: "Administración de registros de DNS en Azure DNS mediante la CLI de Azure 1.0 | Microsoft Docs"
description: "Administración de conjuntos de registros y registros DNS en DNS de Azure al hospedar dominios en DNS de Azure. Todos los comandos de la CLI 1.0 para operaciones en conjuntos de registros y registros."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 307b327e4c04a0461e39930114eb193791cbda9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="9a3e3-104">Administración de registros de DNS en Azure DNS mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9a3e3-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a3e3-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9a3e3-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="9a3e3-106">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9a3e3-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="9a3e3-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9a3e3-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="9a3e3-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a3e3-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="9a3e3-109">En este artículo se muestra cómo administrar los registros de DNS para su zona DNS mediante la interfaz de la línea de comandos (CLI) multiplataforma de Azure, que se encuentra disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="9a3e3-110">También puede administrar sus registros de DNS mediante [Azure PowerShell](dns-operations-recordsets.md) o [Azure Portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9a3e3-111">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="9a3e3-111">CLI versions to complete the task</span></span>

<span data-ttu-id="9a3e3-112">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="9a3e3-113">[CLI de Azure 1.0](dns-operations-recordsets-cli-nodejs.md): la CLI para los modelos de implementación clásica y de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="9a3e3-114">[CLI de Azure 2.0](dns-operations-recordsets-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="9a3e3-115">En los ejemplos de este artículo se supone que ya ha [instalado la CLI de Azure 1.0, iniciado sesión y creado una zona DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="9a3e3-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="9a3e3-116">Introduction</span></span>

<span data-ttu-id="9a3e3-117">Antes de crear registros DNS en Azure DNS, es necesario que comprenda cómo Azure DNS los organiza en conjuntos de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="9a3e3-118">Para más información sobre los registros DNS en Azure DNS, consulte [DNS zones and records](dns-zones-records.md) (Zonas y registros DNS).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="9a3e3-119">Creación de un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="9a3e3-119">Create a DNS record</span></span>

<span data-ttu-id="9a3e3-120">Para crear un registro de DNS, use el comando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="9a3e3-121">Para obtener ayuda, consulte `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="9a3e3-122">Al crear un registro, debe especificar los nombres del grupo de recursos, de la zona y del conjunto de registros, el tipo de registro y los detalles del registro que se están creando.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="9a3e3-123">El nombre del conjunto de registros especificado debe ser un nombre *relativo*; es decir, debe excluir el nombre de zona.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="9a3e3-124">Si el conjunto de registros aún no existe, este comando lo crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="9a3e3-125">Si el conjunto de registros ya existe, este comando agrega el registro que especifique al conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="9a3e3-126">Si se crea un conjunto de registros, se utiliza el valor predeterminado del período de vida (3600).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="9a3e3-127">Para obtener instrucciones sobre cómo usar diferentes TTL, consulte [Creación de un conjunto de registros de DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="9a3e3-128">En el ejemplo siguiente se crea un registro A denominado *www* en la zona *contoso.com* del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="9a3e3-129">La dirección IP del registro A es *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="9a3e3-130">Para crear un registro en el vértice de la zona (en este caso, "contoso.com"), use el nombre de registro "@", incluidas las comillas:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="9a3e3-131">Creación de un conjunto de registros de DNS</span><span class="sxs-lookup"><span data-stu-id="9a3e3-131">Create a DNS record set</span></span>

<span data-ttu-id="9a3e3-132">En los ejemplos anteriores, bien se agregó el registro de DNS en un conjunto de registros existente, bien se creó el conjunto de registros *implícitamente*.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="9a3e3-133">También puede crear el conjunto de registros *explícitamente* antes de agregarle registros.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="9a3e3-134">La DNS de Azure admite conjuntos de registros "vacíos" que pueden funcionar como marcador de posición para reservar un nombre DNS antes de crear registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="9a3e3-135">Los conjuntos de registros vacíos se pueden ver en el panel de control de DNS de Azure, pero no aparecen en los servidores de nombres de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="9a3e3-136">Los conjuntos de registros se crean con el comando `azure network dns record-set create`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="9a3e3-137">Para obtener ayuda, consulte `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="9a3e3-138">Al crear el conjunto de registros explícitamente, podrá especificar las propiedades de este, como el [período de vida (TTL)](dns-zones-records.md#time-to-live) y los metadatos.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="9a3e3-139">Se pueden usar [metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) para asociar datos específicos de la aplicación con cada conjunto de registros como pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="9a3e3-140">En el ejemplo siguiente se crea un conjunto de registros vacío con un TTL de 60 segundos mediante el parámetro `--ttl` (forma abreviada `-l`):</span><span class="sxs-lookup"><span data-stu-id="9a3e3-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="9a3e3-141">En el siguiente ejemplo, se crea un conjunto de registros con dos entradas de metadatos, "dept=finance" y "environment=production", mediante el parámetro `--metadata` (forma abreviada `-m`):</span><span class="sxs-lookup"><span data-stu-id="9a3e3-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="9a3e3-142">Tras haber creado un conjunto de registros vacío, se podrán añadir el registro mediante `azure network dns record-set add-record`, como se describe en [Creación de un registro de DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="9a3e3-143">Creación de registros de otros tipos</span><span class="sxs-lookup"><span data-stu-id="9a3e3-143">Create records of other types</span></span>

<span data-ttu-id="9a3e3-144">Después de haber visto de forma detallada cómo crear registros "A", en los siguientes ejemplos se muestra cómo crear registros de otros tipos compatibles con DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="9a3e3-145">Los parámetros utilizados para especificar los datos del registro varían según el tipo del registro.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="9a3e3-146">Por ejemplo, para un registro de tipo "A", especifique la dirección IPv4 con el parámetro `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="9a3e3-147">Es posible obtener una lista de los parámetros de cada tipo de registro con `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="9a3e3-148">En cada caso, se muestra cómo crear un único registro.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="9a3e3-149">Se agrega el registro al conjunto de registros existente o a uno creado de forma implícita.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="9a3e3-150">Para obtener más información sobre cómo crear conjuntos de registros y definir explícitamente los parámetros de un conjunto de registros, consulte [Creación de un conjunto de registros de DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="9a3e3-151">No se proporciona un ejemplo para crear un conjunto de registros SOA, dado que los registros SOA se crean y eliminan con cada zona de DNS y no lo pueden hacer por separado.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="9a3e3-152">Sin embargo, [el registro SOA se puede modificar, como se muestra en un ejemplo más adelante](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="9a3e3-153">Creación de un registro AAAA</span><span class="sxs-lookup"><span data-stu-id="9a3e3-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="9a3e3-154">Creación de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="9a3e3-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="9a3e3-155">Los estándares DNS no permiten registros CNAME en el vértice de una zona (`-Name "@"`), ni permiten conjuntos de registros que contengan más de un registro.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-155">The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="9a3e3-156">Para más información, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="9a3e3-157">Creación de un registro MX</span><span class="sxs-lookup"><span data-stu-id="9a3e3-157">Create an MX record</span></span>

<span data-ttu-id="9a3e3-158">En este ejemplo, se utiliza el nombre de conjunto de registros "@" para crear el registro MX en el vértice de la zona (en este caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="9a3e3-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="9a3e3-159">Creación de un registro NS</span><span class="sxs-lookup"><span data-stu-id="9a3e3-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="9a3e3-160">Creación de un registro PTR</span><span class="sxs-lookup"><span data-stu-id="9a3e3-160">Create a PTR record</span></span>

<span data-ttu-id="9a3e3-161">En este caso "my-arpa-zone.com" representa la zona ARPA que representa el intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="9a3e3-162">Cada registro PTR establecido en esta zona se corresponde con una dirección IP dentro de este intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="9a3e3-163">El nombre de registro "10" es el último octeto de la dirección IP dentro del intervalo IP que representa dicho registro.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="9a3e3-164">Creación de un registro SRV</span><span class="sxs-lookup"><span data-stu-id="9a3e3-164">Create an SRV record</span></span>

<span data-ttu-id="9a3e3-165">Al crear un [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique el *\_servicio* y el *\_protocolo* en el nombre del conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="9a3e3-166">No es necesario incluir "@" en el nombre del conjunto de registros al crear un conjunto de registros SRV en el vértice de la zona.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="9a3e3-167">Creación de un registro TXT</span><span class="sxs-lookup"><span data-stu-id="9a3e3-167">Create a TXT record</span></span>

<span data-ttu-id="9a3e3-168">En el ejemplo siguiente se muestra cómo crear un registro TXT.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="9a3e3-169">Para más información sobre la longitud de cadena máxima admitida en registros TXT, consulte [Registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="9a3e3-170">Recuperación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="9a3e3-170">Get a record set</span></span>

<span data-ttu-id="9a3e3-171">Para recuperar un conjunto de registros existente, use `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="9a3e3-172">Para obtener ayuda, consulte `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="9a3e3-173">Al igual que sucede con la creación de un registro o conjunto de registros, el nombre del conjunto de registros especificado debe ser un nombre *relativo*, lo que significa que debe excluir el nombre de zona.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="9a3e3-174">También debe especificar el tipo de registro, la zona que contiene el conjunto de registros y el grupo de recursos que contiene la zona.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="9a3e3-175">En el ejemplo siguiente se recupera el registro *www* de tipo A de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="9a3e3-176">Enumeración de conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="9a3e3-176">List record sets</span></span>

<span data-ttu-id="9a3e3-177">Puede mostrar todos los registros de una zona DNS con el comando `azure network dns record-set list` .</span><span class="sxs-lookup"><span data-stu-id="9a3e3-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="9a3e3-178">Para obtener ayuda, consulte `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="9a3e3-179">En este ejemplo, se devuelve todos los conjuntos de registros de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*, con independencia del nombre o del tipo de registro:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="9a3e3-180">En este ejemplo, se devuelven todos los conjuntos de registros que coinciden con el tipo de registro especificado (en este caso, los registros "A"):</span><span class="sxs-lookup"><span data-stu-id="9a3e3-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="9a3e3-181">Adición de un registro a un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="9a3e3-181">Add a record to an existing record set</span></span>

<span data-ttu-id="9a3e3-182">Puede usar `azure network dns record-set add-record` tanto para crear un registro en un nuevo conjunto de registros como para agregar un registro a un conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="9a3e3-183">Para obtener más información, consulte las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="9a3e3-184">Quite un registro de un conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="9a3e3-185">Para quitar un registro de DNS de un conjunto de registros existente, use `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="9a3e3-186">Para obtener ayuda, consulte `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="9a3e3-187">Este comando elimina un registro de DNS de un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="9a3e3-188">Aunque se elimine el último registro de un conjunto de registros, dicho conjunto de registros **no** se elimina.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="9a3e3-189">En su lugar, se conservará un conjunto de registros vacío.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="9a3e3-190">Si desea eliminar el conjunto de registros, consulte [Eliminación de un conjunto de registros](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="9a3e3-191">Debe especificar el registro que desee eliminar y la zona de la que se debe eliminar; para ello, use los mismos parámetros empleados al crear el registro con `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="9a3e3-192">Estos parámetros se describen en las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="9a3e3-193">Este comando solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-193">This command prompts for confirmation.</span></span> <span data-ttu-id="9a3e3-194">Este mensaje se puede suprimir con el modificador `--quiet` (forma abreviada `-q`).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="9a3e3-195">En el ejemplo siguiente se elimina el registro A con el valor "1.2.3.4" del conjunto de registros con el nombre *www* de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="9a3e3-196">Se suprime el mensaje de confirmación.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="9a3e3-197">Modificación de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="9a3e3-197">Modify an existing record set</span></span>

<span data-ttu-id="9a3e3-198">Cada conjunto de registros contiene un [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadatos](dns-zones-records.md#tags-and-metadata)y los registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="9a3e3-199">En las siguientes secciones se explican cómo modificar cada una de estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="9a3e3-200">Para modificar un registro A, AAAA, MX, NS, PTR, SRV o TXT</span><span class="sxs-lookup"><span data-stu-id="9a3e3-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="9a3e3-201">Para modificar un registro existente de tipo A, AAAA, MX, NS, PTR, SRV o TXT, debe agregar primero un nuevo registro y, después, eliminar el existente.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="9a3e3-202">Para obtener instrucciones detalladas sobre cómo eliminar y agregar registros, consulte las secciones anteriores de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="9a3e3-203">En el ejemplo siguiente se muestra cómo modificar un registro "A", de la dirección IP 1.2.3.4 a la 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="9a3e3-204">Para modificar un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="9a3e3-204">To modify a CNAME record</span></span>

<span data-ttu-id="9a3e3-205">Si desea modificar un registro CNAME, utilice `azure network dns record-set add-record` para agregar el nuevo valor del registro.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-205">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="9a3e3-206">A diferencia de otros tipos de registros, un conjunto de registros CNAME solo puede contener un único registro.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="9a3e3-207">Por lo tanto, el registro existente se *sustituye* cuando se agrega el nuevo registro y no hace falta eliminarlo por separado.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-207">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="9a3e3-208">Se le pedirá que acepte esta sustitución.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-208">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="9a3e3-209">En el ejemplo se modifica el conjunto de registros CNAME *www* de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*, para que apunte a "www.fabrikam.net" en lugar de a su valor existente:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-209">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="9a3e3-210">Para modificar un registro SOA</span><span class="sxs-lookup"><span data-stu-id="9a3e3-210">To modify an SOA record</span></span>

<span data-ttu-id="9a3e3-211">Utilice `azure network dns record-set set-soa-record` para modificar el SOA de una zona DNS especificada.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-211">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="9a3e3-212">Para obtener ayuda, consulte `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="9a3e3-213">En el ejemplo siguiente se muestra cómo establecer la propiedad "email" del registro SOA de la zona *contoso.com* del grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="9a3e3-214">Para modificar los registros NS en el vértice de zona</span><span class="sxs-lookup"><span data-stu-id="9a3e3-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="9a3e3-215">El conjunto de registros NS en el vértice de zona se crea automáticamente con cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="9a3e3-216">Este conjunto de registros contiene los nombres de los servidores de nombres de Azure DNS asignados a la zona.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="9a3e3-217">Puede agregar más servidores de nombres a este conjunto de registros NS, para admitir dominios de hospedaje conjunto con más de un proveedor DNS.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="9a3e3-218">También puede modificar el TTL y los metadatos de este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="9a3e3-219">Sin embargo, no puede quitar ni modificar los servidores de nombres de Azure DNS rellenados previamente.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="9a3e3-220">Tenga en cuenta que esto solo se aplica al conjunto de registros NS en el vértice de zona.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="9a3e3-221">Otros conjuntos de registros NS de su zona (como los que se usan para delegar zonas secundarias) se pueden modificar sin restricciones.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="9a3e3-222">En el ejemplo siguiente se muestra cómo agregar un servidor de nombres adicional al conjunto de registros NS en el vértice de zona:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="9a3e3-223">Para modificar el TTL de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="9a3e3-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="9a3e3-224">Para modificar el TTL de un conjunto de registros existente, utilice `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-224">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="9a3e3-225">Para obtener ayuda, consulte `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="9a3e3-226">En el ejemplo siguiente se muestra cómo modificar el TTL de un conjunto de registros, en este caso a 60 segundos:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="9a3e3-227">Para modificar los metadatos de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="9a3e3-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="9a3e3-228">Se pueden usar [metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) para asociar datos específicos de la aplicación con cada conjunto de registros como pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="9a3e3-229">Para modificar los metadatos de un conjunto de registros existente, utilice `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-229">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="9a3e3-230">Para obtener ayuda, consulte `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="9a3e3-231">En el siguiente ejemplo, se muestra cómo modificar un conjunto de registros con dos entradas de metadatos, "dept=finance" y "environment=production", mediante el parámetro `--metadata` (forma abreviada `-m`):</span><span class="sxs-lookup"><span data-stu-id="9a3e3-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="9a3e3-232">Tenga en cuenta que los metadatos existentes se *sustituyen* por los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="9a3e3-233">Eliminación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="9a3e3-233">Delete a record set</span></span>

<span data-ttu-id="9a3e3-234">Los conjuntos de registros pueden eliminarse mediante el comando `azure network dns record-set delete`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-234">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="9a3e3-235">Para obtener ayuda, consulte `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="9a3e3-236">Al eliminar un conjunto de registros también se eliminan todos los registros que contiene.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="9a3e3-237">No se pueden eliminar los conjuntos de registros SOA y NS en el vértice de zona (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-237">You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="9a3e3-238">Se crean automáticamente cuando se crea la zona y se eliminan automáticamente cuando se elimina.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="9a3e3-239">En el ejemplo siguiente se elimina el conjunto de registros con el nombre *www* de tipo A de la zona *contoso.com*, la cual se encuentra en el grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9a3e3-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="9a3e3-240">Se le pide que confirme la operación de eliminación.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="9a3e3-241">Para suprimir este mensaje, utilice el modificador `--quiet` (forma abreviada `-q`).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-241">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a3e3-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a3e3-242">Next steps</span></span>

<span data-ttu-id="9a3e3-243">Más información sobre [zonas y registros en Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="9a3e3-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="9a3e3-244">Aprenda a [proteger las zonas y los registros](dns-protect-zones-recordsets.md) cuando se usa Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9a3e3-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
